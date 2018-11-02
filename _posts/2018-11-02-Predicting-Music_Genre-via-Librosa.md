---
layout: post
title: Predicting Musical Genre from Sound File Features Extracted via Librosa
---

Back when I was a younger man and crossing the country playing music for screaming crowds (really, making occasional weekend drives to Wisconsin to play at a bar for six other people and drink some free Blatz), I kept having the same frustrating conversation over and over. It went something like this:

Person: Oh cool, you play in a band? What kind of music do you play?
Me: Well it's sort of like an alt-pop kind of thing. Maybe sort of like rock too I don't know.
Person: Alt-pop? I have no idea what that means.
Me: Hm. Well someone once told me we sounded like if Cat Stevens joined the New Pornographers and they all decided they just wanted to make people dance.
Person: ... I can't even imagine what that sounds like.
Me: Coincidentally our lead singer actually did recently convert to Islam, too.
(Person wanders away, bewildered)

For a person with mildly debilitating social anxiety, this was pretty stressful. It's not actually why I don't play with that band anymore, and I didn't actually decide to learn data science solely to answer this question, but for the sake of this post's narrative let's pretend that's how it went. (And for the record, that weirdly specific description is bizarrely accurate.)

Anyway, onto the data science!

The [Free Music Archive](http://freemusicarchive.org/) is a collection of more than 100,000 downloadable music tracks with associated metadata that includes various sonic features extracted from the tracks via a relatively new Python library called [Librosa](https://librosa.github.io/librosa/). The majority of these tracks are categorized into 16 top-level genres, resulting in a very large dataset well-suited to building a model for categorizing music into genres based on its spectral and rhythmic features.

After downloading this dataset from the [FMA GitHub](https://github.com/mdeff/fma) and cleaning up the files (they were in pretty great shape, but for simplicity's sake I removed all of the tracks that had more than one top-level genre and used only the nine largest genres in my model), I trained and tuned a variety of supervised learning models, settling on a scikit-learn XGBoost model as my best performer, achieving about 60% accuracy across 9 possible genres (much better than the 11% accuracy that would be obtained by random guessing). However, this model took hours to run on my 40,000-track training set, making tuning laborious. Furthermore, my goal was to develop a web app that would use the model to determine the genre of any uploaded mp3 file, for which I really needed a more efficient model.

To that end, I ran a Principal Component Analysis to reduce my 500+ features to 15 features. This didn't sacrifice much information, as my 15 features captured just about all of the variance of my original 500+ features (greater than 99.99%). This small information loss resulted in huge efficiency gains -- the model ran in less than 20 minutes compared to several hours previously.

In order to finally be able to answer the question about what my band sounded like, I pickled the model and my PCA transformation and built a webapp via Flask that allowed a user to upload an mp3 file, then used Librosa to extract the necessary features from that file, transformed the features via my existing PCA transformation, and then ran the transformed features through the model to output the mp3's genre. For a little extra fun, I had the model output its level of confidence in its categorization (in the form of the specific probability it assigned to the most likely genre).

After much wrangling with Flask, my app gave me the information I needed years ago: it is 75% likely that my band is rock! Glad that's settled after all these years.

I'll be posting a link to the web app here soon -- it's going up on AWS as soon as I've made the upload process secure enough for public use.

In a follow-up post I'll describe some of the challenges I faced due to the imbalanced categories in my training set (between 14,000 and 1,200 tracks per genre) and how the presence of multiple tracks from many artists caused oversampling to fail to compensate for this imbalance.

As with my earlier project, my [None-More-Black repo](https://github.com/bartolone/none-more-black) has more findings and code from this project, and will host my continued data science investigations into music genres and linguistic characteristics.
