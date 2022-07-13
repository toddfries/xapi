lets play with twitter api

Go get a deveoper key/secret, put in a conf file like so:

$ mkdir -p $HOME/.config/tapi
$ cat <<EOF > $HOME/.config/tapi/tapi.conf
[creds]
consumer_key = <consumer_key>
consumer_secret = <consumer_secret>
EOF

Now get the access token and secret:

$ oauth
Authorize this application at: https://api.twitter.com/oauth/authorize?oauth_token=<magic autogen string>
Then, enter the returned PIN number displayed in the browser: <pincode from browser>

access_token.......: <access_token>
access_token_secret: <access_token_secret>
...
$ cat <<EOF >> $HOME/.config/tapi/tapi.conf
access_token = <access_token>
access_token_secret = <access_token_secret>
EOF

$ tweets unix2mars
...
0 2022-07-13T20:33:03.000Z @unix2mars RT Another level nested again. (1547318208583143425, Re 1547318135841226753)
    1 2022-07-13T20:32:46.000Z @unix2mars RT Reply of reply test. (1547318135841226753, Re 1547318006996508672)
        2 2022-07-13T20:32:15.000Z @unix2mars RT Reply test. (1547318006996508672, Re 1547317865640038402)
            3 2022-07-13T20:31:41.000Z @unix2mars This is a test. Please ignore. (1547317865640038402)
...
