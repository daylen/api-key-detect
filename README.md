# API Key Detect

This script scans a codebase for API keys and passwords. Perfect for scrubbing private data from source code that you will be open sourcing.

## How to use
Usage: `python api_key_detect.py [PATH_TO_DIRECTORY]`

## Example output
```
Scanning directory: /Users/daylenyang/Developer/instavote
Ignoring: ['.git', 'node_modules', 'bower_components', '.sass-cache', '.png', '.ico', '.mov']
For tokens with minimum entropy ratio: 0.5
/Users/daylenyang/Developer/instavote/server.js : Line 61 : Entropy 0.6
		secret: '4KguaGRREDACTED',

/Users/daylenyang/Developer/instavote/app/email.js : Line 11 : Entropy 0.590909090909
		pass: '6S6NELREDACTEDREDACTED'

/Users/daylenyang/Developer/instavote/app/payments.js : Line 12 : Entropy 0.6875
	stripe = require('stripe')('sk_test_4M2RoqT5REDACTEDREDACTED');

/Users/daylenyang/Developer/instavote/app/payments.js : Line 14 : Entropy 0.625
	stripe = require('stripe')('sk_live_4M2R5LE8REDACTEDREDACTED');

/Users/daylenyang/Developer/instavote/app/payments.js : Line 106 : Entropy 0.6875
		return 'pk_test_4M2RKB8nREDACTEDREDACTED';

/Users/daylenyang/Developer/instavote/app/payments.js : Line 108 : Entropy 0.53125
		return 'pk_live_4M2RcGm5REDACTEDREDACTED';

/Users/daylenyang/Developer/instavote/views/support.jade : Line 16 : Entropy 0.545454545455
					iframe(class="embed-responsive-item" src="//www.youtube.com/embed/7Y4ADGqnQek?rel=0" frameborder="0" allowfullscreen)
```

## Configuration
Chances are you'll need to tweak some of the parameters to properly scan your code. At the top of the script are some options:

- The `ignored` list: add patterns for filenames that you want to ignore
- `api_key_min_entropy_ratio`: How much entropy is needed to say it's an API key. Raising this number catches fewer keys. Lowering it will catch more keys but introduce false positives.

## How it works
Really stupid simple algorithm, it just checks to see how much variance there is character-to-character in every line of every file in a directory. On the plus side, it's language-agnostic.

## License
GPLv3.
