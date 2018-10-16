---
layout: post
title: Predicting Album Ratings via Album Name Metalness
---

Bands make linguistic choices when writing lyrics, naming songs and albums, and choosing the name of their
band. Hopefully, these choices signal the band's aesthetics to potential listeners so that they find
their audience. From my perspective, this aesthetic signaling is valuable in helping to
sort through the many thousands of albums available on the Internet to find those that I am most likely to enjoy.

I tend to have strong positive reactions to certain words that signify an aesthetic I am likely to enjoy
(really, anything that sounds like Dungeons and Dragons will probably do the trick, especially if there's a
wizard involved). I got to wondering if album names could actually help bands find listeners who would share
their aesthetics and therefore be more likely to enjoy their music. But how to quantify the aesthetic?

Thankfully, Iain Barr has already created a "metalness index" for 10,000-some words based on their relative
frequency in metal lyrics compared to other forms of writing [(full details in his blog post here.)](http://www.degeneratestate.org/posts/2016/Apr/20/heavy-metal-and-natural-language-processing-part-1/)

I used Iain's metalness index to create metalness scores for approximately 7,500 metal album titles as well as
for the song titles on each album and the name of each band, and then ran a series of linear regressions to
determine if metalness scores could predict the ratings that metal fans give to those albums.

No. Nuh-uh. Not even a little. (The "best" model using only metalness scores accounted for approximately
0.1% of the variance in album ratings.)

In other words, it doesn't seem to matter what you name your band, your album, or your songs, people are going to like your music (or not) based on less-obvious factors like, you know, if it's any good or not.

(I'd probably give a bonus point per wizard myself, but I seem to be in the minority.)

Still, I learned a few things during my investigation into the album ratings on [metalstorm.net](metalstorm.net). For one, user ratings tended to be higher for albums released in earlier years:

![Album ratings by year of release]({{ site.url }}/images/year_scatter_all.png)

However, that vertical line represents Metal Storm's founding in 2000 -- and if you look at the albums they reviewed retrospectively, they are nearly all classics by the likes of Black Sabbath, Led Zeppelin, and Iron Butterfly. Release year post-1999 didn't have nearly as much of a relationship to album ratings.

(If you're wondering about that low rating in the late '80s, that would be when a renowned extreme metal band named Celtic Frost tried to get some of that Bon Jovi money by recording a glam album. It ... did not work.)

The only other bit of album metadata that seemed related to review scores was the number of users reviewing an album:

![Album ratings by number of user reviews]({{ site.url }}/images/user_reviews_scatter.png)

It seems pretty self-evident that users would be more likely to review albums that were widely acclaimed, even if they themselves hated it.

(Two more outliers here, where hundreds of users reviewed, and generally hated, albums -- if you guessed that those were the album Metallica recorded with Lou Reed and their St. Anger album that everyone hated, [invisible oranges](http://theblekgoat.com/invisible-oranges-become-fully-visible/) to you.)

My [None-More-Black repo](https://github.com/bartolone/none-more-black) has more findings and code from my investigation of how metalness scores (don't) relate to album ratings. Stay tuned to that space for more heavy investigations.
