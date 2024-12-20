listargs="list.fields=created_at,follower_count,member_count,name,owner_id,private&expansions=owner_id&user.fields=connection_status,created_at,description,entities,id,location,most_recent_tweet_id,name,pinned_tweet_id,profile_banner_url,profile_image_url,protected,public_metrics,receives_your_dm,subscription_type,url,username,verified,verified_type,withheld"

curl "https://api.twitter.com/2/lists/1729635365319802902?${listargs}" \
	-H "Authorization: Bearer $BEARER_TOKEN"

# free, 1/15m
xposts -a get2 "lists/1729635365319802902?${listargs}"

listargs="list.fields=created_at,description,follower_count,id,member_count,name,owner_id,private&expansions=owner_id&user.fields=affiliation,connection_status,created_at,description,entities,id,location,most_recent_tweet_id,name,pinned_tweet_id,profile_banner_url,profile_image_url,protected,public_metrics,receives_your_dm,subscription_type,url,username,verified,verified_followers_count,verified_type,withheld"
xposts -a get2 "lists/1490757476332945413/list_memberships?${listargs}"

# write a post
xposts -c foo.conf -w test
# write a reply post
xposts -c foo.conf -w test -W pid
# write a quote post
xposts -c foo.conf -w test -Q pid

# show bookmarks
xposts -b 

# arbitrary v2 get
xposts -a get2 users/by/username/elonmusk

# arbitrary v1 get
xposts -J account/verify_credentials

# -r 5 # 5 posts in results
# -l 1 # 0 = no like data, 1 = like data

# show a single users stats
xposts -s unix2mars

# show a list of users stats
# free, 3/15m, 96/24h
xposts -S unix2mars elonmusk

# show lists of a user
xposts -L Scobleizer

# arbitrary v2 post
xposts -p "dm_conversations/with/218538224/messages;text=HelloWorld"

# add a bookmark
xposts -B :postid

# show a singular post
# free, 1/15m
xposts -T :postid
xposts -a get2 "posts/1732923352?tweet.fields=community_id"

# show followers
# !free
xposts -a get2 "users/218538224/followers?user.fields=id,location,public_metrics,subscription_type,verified,verified_type&tweet.fields=id,media_metadata,organic_metrics,public_metrics,scopes,source"

# show owned lists
# free, rate 1/24h
xposts -a get2 "users/218538224/owned_lists"

# show followers of a list
# !free
xposts -a get2 "lists/1616593562979778562/followers"

# list members of a list
# free, 1/15m
xposts -a get2 "lists/1616593562979778562/members"

# add member to list
# free, 1/15m
xposts -p "lists/1733137040718360773/members;user_id=1312511"

# look up a list
# !free
xposts -p "lists/1733137040718360773"

# set a list private
# try 20241130 or later
xposts -a get2 "lists/1733137040718360773;id=1733137040718360773;private=true"

# delete a post
# free, 17/24h
xposts -a delete posts/1868694921458385046

# list users I've muted
# free, 1/24h
xposts -a get2 users/218538224/muting
