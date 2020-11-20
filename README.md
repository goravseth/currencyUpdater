# currencyUpdater
some simple code to automate updating of currencyType records (the spot conversion rate) using openexchangerates.com.  you can setup a free account with openexchanagerates that has 1,000 calls per month, which is plenty.  I run it once daily - you could do it more often if helpful.

This uses a named credential in your org called OpenExchangeRates though all it does is set the callout endpoint, as the auth is via an api key stored in a custom metadata type.

For reasons only known to Steven Tamm, currencyType records cannot be updated via apex - only via the API.  I chose a REST callout, just because I could.

As this runs via a scheduled job, I beleive I had issues passing the session ID to the callout.  Worked fine from anonymous apex but not from scheduled job.

I was able to use a connected app + auth provider + named credential (and maybe requires a remote site setting) to authenticate.

1. create connected app
2. create auth provider, type = salesforce, setting the public and private key from the connected app manually (dont use the default values)
3. set callback url on connected app to the callback url listed by the auth provider
4. create named credential using auth provider in step 2
5. use named credential in callout

poof.  currencies, updated daily.  



