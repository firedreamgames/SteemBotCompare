## Real time data addition to SteemBotCompare
webpage:https://steembotcompare.neocities.org/

![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514843349/wmhnw8lnqu775ol81f2k.png)

### Introduction

[SteemBotCompare](https://utopian.io/utopian-io/@firedream/steembotcompare-steem-js-website-for-bot-comparison) is a program that compares bots that are active in Steem.
User can select up to 7 different upvote bots to compare with real-time data.
New properties added to the program.

### New Added Features
* #### Upvote quantity:
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514843715/y13asib6i2vouiajqome.png)
This feature calculates how many times the bot has upvoted.

This is done mainly with script :


> var release = steem.api.streamTransactions('head', function(err, result) 
> {
> if(result.operations["0"]["0"]=='vote')   //*check if the operation is a voting*
> {
> if (result.operations["0"][1].voter==botNo1) //*check if the voter is concerning bot*
> {
> botvot1=botvot1+1;   //*increase the vote counter*
> bottable.rows[7].cells[1].innerHTML =botvot1;  //*write the vote qty. on the table* 
> };

The update is done with every voting operation on steem.

* #### Total Strength Used
Generally upvote bots finish voting when their used strength is approximately 100%
This is using of %2 of their total strength.
So if an upvote bot starts upvoting with %100, at the end of voting session the total stregth will be %98.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514844459/svtm6u1maami9zmq4fcu.png)
When this indicator is close to 100% it will mean that the bot will finish voting soon.
The script for finding this is similar : 

> var release = steem.api.streamTransactions('head', function(err, result) 
> {
> if(result.operations["0"]["0"]=='vote')   //*check if the operation is a voting*
> {
> if (result.operations["0"][1].voter==botNo1) //*check if the voter is concerning bot*
> {
> botstr1=botstr1+(result.operations["0"][1].weight/100); //*calculate cumulated power use*
> bottable.rows[8].cells[1].innerHTML ='% '+botstr1.toFixed(3);  //*write the cumulative on the table* 
> };

* #### Average Upvote Strength

This is average upvote power used per bidder.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514845846/okucmfzp3yus3vujqush.png)

Calculated by :
> botav1=botstr1/botvot1;

Written to the table :
> bottable.rows[9].cells[1].innerHTML ='% '+botav1.toFixed(3);

* #### Minimum Upvote Strength
This feature is very important indicator. This shows how much the upvote bot upvotes the posts at the minimum bid.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514876557/tamne4ku9bpilgmxdz7j.png)

All the upvote bots have minimum bids.
When you send the minimum bid, it upvotes with a certain %.
This percentage changes according to the bid you make.
Forexample, if the bot minimum bid is 1 SBD, this indicator shows how much % of upvote this bot gives when you send 1 SBD to the bot.
This also means if you send 2 SBD, theorotically you will receive two times of % upvote from the bot.
 The code managing this is as follows : 

> var botmin1=100 //*maximize the minupvote variable to find the minimum*
> var release = steem.api.streamTransactions('head', function(err, result) 
> {
> if(result.operations["0"]["0"]=='vote')   //*check if the operation is a voting*
> {
> if ((result.operations["0"][1].weight/100)<botmin1) // *check if the result is minimum*
> {
> botmin1=(result.operations["0"][1].weight/100); // *write the value to variable if it is minimum*			
> }
>bottable.rows[10].cells[1].innerHTML ='% '+botmin1.toFixed(3); // *write the value to table*

>}

* #### Maximum Upvote Strength
This indicator is put to see if there is a difference of payout as percentage when you send more bid to a bot.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514878894/vvi3vbsvimyb0dcmfcfz.png)
 The script managing this is as follows : 

> var botmax1=0 //*minimized variable*
> var release = steem.api.streamTransactions('head', function(err, result) 
> {
> if(result.operations["0"]["0"]=='vote')   //*check if the operation is a voting*
> {
> if ((result.operations["0"][1].weight/100)>botmax1) // *check if the result is maximum*
> {
> botmax1=(result.operations["0"][1].weight/100); // *write the value to variable if it is maximum*			
> }
>bottable.rows[11].cells[1].innerHTML ='% '+botmax1.toFixed(3); // *write the value to table*

>}

The use of minimum and maximum values is best explanied by an example :

The analysis time is 02.01.2018 - 07:10 UTC Time.

This was the time "pushup" bot was at voting cycle.

After a quick analysis of 260 seconds it was observed that the minimum and maximum vote strengths were as follows :
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514877967/udxbcvz5opa4a7hkwodb.png)
Min : 0.32%
Max : 9.86%

Taking a look at [steemd](https://steemd.com/@pushup):
"pushup" upvated following post with minimum (0.32%)
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514878115/pefex9bpecm3llpq76hl.png)
Take a quick search on [steemd](https://steemd.com/@pushup) we find :
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514878190/bzcypncdwoxur9vel6gr.png)
The user have sent 0.1 SBD ( minimum bid for this bot ) to pushup and he got upvoted.

So converting it to unit SBD ( how much vote could we get if we sent 1 SBD ) we find :
%0.38 / 0.1 SBD = 3.8%
Theorotically, if we send 1 SBD to this bot we would be upvoted by 3.8%.

Now let's check if this is true :
At [steemd](https://steemd.com/@pushup) we find :
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514878409/ksjzlvgoey9fqtlhtqv1.png)
this post is upvoted at maximum (9.86%)
Looking at the post :
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514878518/c10dnepnb56x7kwwp2lr.png)
This user sent 3SBD to pushup.
Let's again convert it to upvote / unit SBD
9.86% / 3 SBD = 3.29%

This result more or less approves our theory but there is a slight difference which I think comes from rounding numbers.

* #### Last upvote time
The upvoting bots are working in cycles. After upvoting for %100 ( which consumes their %2 of voting power ) they go into a resting state to recover their upvoting power to be ready for new voting.
This cycle generally requires 2.4 hours ( 8640 seconds).
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514879545/mss2levh99q1acp9wuhq.png)
 The script managing this is as follows ( thank you @stoodkev for all the steem.js documents ) : 

> steem.api.getAccounts([botNo1], function(err, response){
> var secondsago = (new Date - new Date(response[0].last_vote_time + "Z")) / 1000;

This is again theorotical but looking at this time, you can predict more or less when the bot will start upvoting again.

* #### Voting Power
This is a real time indicator, with how much power is the bot voting.
According to my observations the upvote bots, with a little exeptions are strictly obeying their upvoting - resting cycles so that all the upvotes are made between %100 - %97 power of the bot maintaining a very little income difference.
But it is always important to prove that in case there is something wrong, a disturbance with the bot.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514880489/ymrkwhtz2k8n5erdxluc.png)
The code for this : 
> steem.api.getAccounts([botNo1], function(err, response){
> var secondsago = (new Date - new Date(response[0].last_vote_time + "Z")) / 1000;
> var vpow = response[0].voting_power + (10000 * secondsago / 432000);
> vpow = Math.min(vpow / 100, 100).toFixed(2);
This is also an indicator to be used with "last voting time" since the bots start voting again when their voting power is close to %100.

* #### Voting Weight of the Bot
This is the most important indicator in the bot analysis.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514880946/dudabf4m3mmxagun0cms.png)
If 2 bots are voting you at %0.38 the difference in their voting weight will directly effect your income.

Let's take the example with pushup bot that we previously written.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514881019/iww8ajahshxflopln5kb.png)

We have seen that pushup bot is giving 3.8% upvote per 1 SBD sent.
The voting weight of pushup bot is 326,407 steems at the time of analysis. 

Now consider an other bot giving us %0.5 upvote per 1 SBD sent.
How can we conclude which bot is better ?
To tell which bot is better we have to check the voting weights.

If the second bot has 2,500,000 steems then a comparison would be made as follows :
pushup is giving --> %3.8 x 326,407 =12403 vote.steem
bot2 is giving -->      %0.5 x 2,500,00 = 12500 vote.steem
Here we can conclude that infact both bots gives you the same income / SBD.

The code to calculate the voting weight is a bit complex.
I recommend a very good tutorial prepared by @stoodkev with [this link.](https://utopian.io/utopian-io/@stoodkev/steemjs-for-dummies-2-calculate-the-user-s-steem-power)
I also used this tutorial.

### Conclusion
With this web application https://steembotcompare.neocities.org/ you can directly deep-dive into the analysis of the bots on real time and you can conclude yourself with *facts and data* which upvote bot to use.
You can also use this application to further analyse bot behaviors and share your own analysis on Steemit.
 The GitHub link for the project : https://github.com/firedreamgames/SteemBotCompare
Link for index.html source code : https://github.com/firedreamgames/SteemBotCompare/blob/master/index.html
Link for the website : https://steembotcompare.neocities.org/ 
