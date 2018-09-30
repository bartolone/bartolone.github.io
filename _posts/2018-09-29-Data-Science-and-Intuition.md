---
layout: post
title: First Metis project -- combining data science with intuition
---

After week 1 of 12 of the Metis Data Science Bootcamp, the first of our five projects is done. This one was a bit different than the remaining projects, in that it was a group project and the topic was assigned, but I think it ended up illustrating an interesting phenomenon that I expect to see again during my data science career.

My team started out by identifying what we thought were reasonable answers to the problem, and then used the data to check the reasonableness of our answers. As it turns out, the data supported our recommendations. I feel like most descriptions of data science involve amazing data-based insights, but in this case, the data science confirmed that we already had a pretty solid handle on the problem before consulting the data.

More on that in a moment, but first I want to acknowledge my awesome teammates Gabe and Charlie. Charlie took the opportunity to dig into web scraping techniques using Scrapy (I'm not sure how it's supposed to be pronounced but I insist on the most adorable diminutive pronunciation) even though scraping wasn't required -- but we're all here to learn, so why not? Gabe has a keen eye for data structures and code organization and provided some critical insights and well thought-out code.

Actually, my two teammates did 98% of the coding work between them, while I served as a sounding board and focused on our presentation. That said, I'm pretty geeked about the few lines I did contribute -- if you want to talk about the pandas shift() function come find me. It felt a little weird to lean into the parts of the work I'm already comfortable with, but I'll have plenty of time to dig into python over the next 11 weeks.

Back to the project -- our assigned task was to use MTA subway data to help a fictional organization supporting women in technology optimize how they place their street teams at NYC subway stations in advance of their summer gala. We were asked to optimize for promoting awareness, driving attendance to their gala, and growing their donor pool.

I think our team's key success is that we spent day one (of our 4.5 days) talking through the problem rather than diving straight into the data, and asking questions of our 'clients' (our redoubtable instructors, Lara and Alice). While they deferred most of our questions, they did provide the gala location (Manhattan's Lower East Side), which led directly to our key insights.

We talked through how to make sure that our client reached not just the most people, but the most of the right people -- those who would be interested in supporting their cause, attending their gala, and donating to the organization. We therefore prioritized areas of New York that were relatively easy to get to the Lower East Side from (by subway), had high concentrations of tech companies (not just Manhattan's Silicon Alley but the nearby Brooklyn Tech Triangle), and contained high concentrations of wealthy households (as measured by Census data). In practice, these three criteria converged on similar areas, and we manually identified 19 subway stations that met all or most of our criteria.

It was only after this that we dug into the MTA data itself to see if the 19 stations we identified as priority targets were actually reasonable recommendations. That's not to give our analysis short shrift -- I think my teammates and I were thoughtful about how we used the data, eventually determining the mean hourly ridership of each station over previous months that were similar to the month our client's street teams would do their work. (We used mean hourly ridership because, while the turnstile-level data was usually reported in four-hour intervals, stations were on different hourly reporting schedules and many turnstiles had reporting gaps that left us with weekly or longer reporting periods.) In the end, though, the stations we identified at the beginning were generally high enough in the ranked list of all MTA stations (again, by mean hourly ridership) to support their usefulness as targeted stations. Some stations had higher passenger volume, but I stand by our assumption that it's better to send street teams to the third-most busy station that is near tech companies and within a wealthy area than to Times Square, where they're likely to encounter tourists rather than their intended audience.

I'm sure there will be plenty of future projects in which the data does the speaking, but our first project demonstrated that sometimes data science can be used instead to confirm (or not!) that you're already on the right track.

Onwards!
