---
layout: post
title: Predicting Album Ratings via Album Name Metalness
---

Bands make linguistic choices when writing lyrics, naming songs and albums, and choosing the name of their band. Hopefully, these choices signal the band's aesthetics to potential listeners so that they find their audience.

I tend to have strong positive reactions to certain words that signify an aesthetic I am likely to enjoy (really, anything that sounds like Dungeons and Dragons, especially if there's a wizard involved). I got to wondering if good album names could actually help facilitate connections between bands and potential fans. But how to quantify the aesthetic?

Thankfully, Iain Barr has already created a "metalness index" for 10,000-some words based on their relative
frequency in metal lyrics compared to other forms of writing [(full details in his blog post here.)](http://www.degeneratestate.org/posts/2016/Apr/20/heavy-metal-and-natural-language-processing-part-1/)

I used Iain's metalness index to create metalness scores for approximately 7,500 metal album titles as well as
for the song titles on each album and the name of each band, and then ran a series of linear regressions to
determine if metalness scores could predict the ratings that metal fans give to those albums.

Before modeling, I checked to make sure that the metalness scores passed the eyeball test. I actually calculated them a few different ways -- using the mean metalness score of the words in the album titles meant that single-word titles (or titles with only one word in the index) had more extreme scores, and the top metalness list was comprised of albums titled "Burn" (the most metal word in the index). Using the sum of metalness scores privileged long album names, which led to some slightly silly results. I was most happy with the ratings derived from a compromise method that divided the sum of metalness scores by half of the number of words in the title. Here's what they looked like:

**The five most metal album names:**
* Rage Of The Blood Beast
* Sword Of Revenge
* Tears And Ashes
* Burn Me Wicked
* Bury The Ashes

That seems pretty legit, doesn't it? The first two speak to me more than the other three, but the right ingredients are there for sure, and we have a variety of highly metal words represented.

**The five least metal album names:**
* Crumb's Crunchy Delights Organization
* Doomsday For The Deceiver 20th Anniversary Special
* Nato Per Ragioni Ignote
* Carte Blanche
* District Of Dystopia

These also look about right to me. It's a little weird that the third album is in Italian (it translates to Born for Unknown Reasons), but the metalness index interpreted the first word as "NATO", which is pretty un-metal (metalness score: -3.66). The last entry illustrates a quirk of the index: un-metal scores are negative, and have a larger absolute value than the highest metalness scores (scores range from -5.99 to 4.15). District is a fairly un-metal word (-4.35), whereas dystopia, despite sounding pretty metal, was not in the index at all (but even if it was, it could not have balanced out the score for "district").

So, since it looks to me like these metalness scores are representing something, back to the question at hand -- does the metalness of album titles (or song titles or band names) have any relationship to the ratings of that album?

...

No. Nuh-uh. Not even a little. (The "best" model using only metalness scores accounted for approximately
0.1% of the variance in album ratings.)

...

![Heavy metal wizard](https://litreactor.com/sites/default/files/imagecache/header/images/column/headers/saruman-rocks.jpg)

(I'd probably give a bonus point per wizard myself, but I seem to be in the minority.)

In other words, it doesn't seem to matter what you name your band, your album, or your songs, people are going to like your music (or not) based on less-obvious factors like, you know, if it's any good or not. So you may as well name your album The Committee Chairman’s Particularly Literary Secretary (the 4th, 9th, 1st, 16th, and 3rd-least metal words in the index).

Still, I learned a few things during my investigation into the album ratings on [metalstorm.net](metalstorm.net). For one, user ratings tended to be higher for albums released in earlier years:

![Album ratings by year of release]({{ site.url }}/images/year_scatter_all.png)

However, that vertical line represents Metal Storm's founding in 2000 -- and if you look at the albums they reviewed retrospectively, they are nearly all classics by the likes of Black Sabbath, Led Zeppelin, and Iron Butterfly (that's right). Release year post-1999 didn't have nearly as much of a relationship to album ratings.

(If you're wondering about that low rating in the late '80s, that would be when a renowned extreme metal band named Celtic Frost tried to get some of that Bon Jovi money by recording a glam album. It ... did not work.)

The only other bit of album metadata that seemed related to review scores was the number of users reviewing an album:

![Album ratings by number of user reviews]({{ site.url }}/images/user_reviews_scatter.png)

It seems pretty self-evident that users would be more likely to review albums that were widely acclaimed, even if they themselves hated it.

(If you guessed that the two albums that hundreds of reviewers nearly universally hated were the album Metallica recorded with Lou Reed and their much-maligned St. Anger, [invisible oranges](http://theblekgoat.com/invisible-oranges-become-fully-visible/) to you.)

My [None-More-Black repo](https://github.com/bartolone/none-more-black) has more findings and code from my investigation of how metalness scores (don't) relate to album ratings. Stay tuned to that space for more heavy investigations.
