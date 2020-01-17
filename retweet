var Twit = require('twit')
var T = new Twit({
    consumer_key:         'mB3uteLcwsRiL63uiKiUVkSgz',
    consumer_secret:      'GYdJI9SrJYdnPMZeZL1DMSpjic4VmiC00im6DtbB34bBLyxYr5',
    access_token:         '799149391449686016-E17qyV1kRPnUqhYVPQUJEP8Xs0IixN0',
    access_token_secret:  'DiDzSi4ir2erGfDt2qGtXGaCSnqWOHmXrswE81M2k1hw8',
})


//retweet leading political candidates (Bernie Sanders, Joe Biden, Elizabeth Warren)
var users = ["29442313", "939091", "970207298"]
var stream = T.stream('statuses/filter', {follow: users});

stream.on('tweet', function (tweet) {
    if (users.indexOf(tweet.user.id_str) > -1) {
        console.log(tweet.user.name + ": " + tweet.text);
        T.post('statuses/retweet/:id', { id: tweet.id_str }, function (err, data, response) {
            console.log(data)
        })
    }
})

//retweet
let retweet = function() {
    let params = {
        q: '#politics',
        result_type: 'recent',
        lang: 'en'
    }

    // search through all tweets using our params and execute a function:
    T.get('search/tweets', params, function(err, data) {
        if (!err) {
        for (let i = 0; i < 4; i++) {
        let rtId = data.statuses[i].id_str;
        T.post('statuses/retweet/:id', {
            id: rtId
        }, function(err, response) {
            if (response) {
            console.log('Successfully retweeted');
            }
            if (err) {
            console.log(err);
            }
        });
        }
    }
        else {
        console.log('Could not search tweets.');
        }
    });
}
retweet();
setInterval(retweet, 600000);
