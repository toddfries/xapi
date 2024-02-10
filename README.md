lets play with the 𝕏 api

Go get a deveoper key/secret, put in a conf file like so:

```
$ mkdir -p $HOME/.config/xapi
$ cat <<EOF > $HOME/.config/xapi/xapi.conf
[creds]
consumer_key = <consumer_key>
consumer_secret = <consumer_secret>
EOF
```

Now get the access token and secret:

```
$ oauth
Authorize this application at: https://api.twitter.com/oauth/authorize?oauth_token=..magic..autogen..string..
Then, enter the returned PIN number displayed in the browser: <pincode from browser>

access_token.......: <access_token>
access_token_secret: <access_token_secret>
...
$ cat <<EOF >> $HOME/.config/xapi/xapi.conf
access_token = <access_token>
access_token_secret = <access_token_secret>
EOF
$ xposts unix2mars
...
0 2022-07-13T20:33:03.000Z @unix2mars RT Another level nested again. (1547318208583143425, Re 1547318135841226753)
    1 2022-07-13T20:32:46.000Z @unix2mars RT Reply of reply test. (1547318135841226753, Re 1547318006996508672)
        2 2022-07-13T20:32:15.000Z @unix2mars RT Reply test. (1547318006996508672, Re 1547317865640038402)
            3 2022-07-13T20:31:41.000Z @unix2mars This is a test. Please ignore. (1547317865640038402)
...
```

With the new tiers of api access, free only does:

  account/verify_credentials
  account/settings
  users/me
  tweets
  media/metadata/create
  uploads.twitter.com/1.1/media/upload

Let me know if I missed any!

With 'xposts' this currently looks like:

 # must be the user granting the key
  xposts -s username
  xposts -j users/me
  xposts -w "hi there cli tweet"
   .. displays:
   https://x.com/username/status/12345
  xposts -w "replying to my cli tweet" -W 12345
  xposts -w "reply post with two images" -W 12345 -I foo.jpg,fun.jpg
  xposts -w "reply post with four images with descriptions" -W 12345 -I 1.jpg="one",2.jpg="two",3.jpg="three",4.jpg="Four"
