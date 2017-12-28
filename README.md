# SteemBotCompare
Comparison of transaction and usage of user selected bots in Steem

webpage:https://steembotcompare.neocities.org/
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514495075/uc5kow4elcqtigrpcwns.png)



### INTRODUCTION
A single page HTML-JavaScript website that makes the analysis of transactions made by the Steemians to the bots.
As logic,it can detect every transaction but the use of this website is particularly follow the popularity of the bots and help users
decide with *facts and data* which bot to use in a certain time interval.

### FEATURES

 _**1. Bot Selection :**_
There are 7 preselected bots.
User can change the bots by writing their name in the text boxes
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514495332/nsk57qcflfnr3fqvykez.png)

 _**2. Start Analysis :**_
Pushing the "Start Analysis" button starts the analysis of the Steem blockchain
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514495446/opubzhohhpa2au5sm5tf.png)
When the analysis starts several things happen :
* Time counter starts and you start to see all the transactions made in Steem blockchain.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514495628/mw7tsmtkphwdtdxabesw.png)

* The transaction quantity starts to display in the table.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514495732/rovfjve4zhugodnsv8dp.png)
This is the number of all SBD and Steem transactions, not only to bots but all.
This data may be important for the future analysis since it is meaningful with time.
As of 29.12.2017 in 811 seconds there happened 304 transactions inside Steem, to Steem or out of Steem.
So the ratio is approximately 1 transaction/3 seconds.
* The transactions to the bots start being displayed.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514496063/vyj96d0nr25g7hvfssan.png)
In above example we can conclude that :
"upme" bot have received 6 of 107 total transactions
 The total amount of 6 transactions - as SBD- is 18.5 SBD
No transactions are made with Steem ( some bots accept payment with Steem )
Total amount of transactions received by "upme" bot is 18.5 SBD.

The formula is converting Steem to SBD as 1/3 ratio.
This is approximation.
Total amount Received in SBD is calculated as SBD receival + Steem Receival/3

Data for other 6 bots are also visible in the table.

 _**3. Change Bot Name :**_
While analysis, to change the name of the bot and compare another one, user should enter the name of the bot to the box ( any of them )
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514496658/alonopatasswtmadh2p3.png)
Then hit "Start Analysis" button again.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514496705/zjztwsxsnhe8jexas2vl.png)
This will reset the time and transaction counter and start analysis from zero.

 _**4. WebSite**_
Currently the web site is in a free-hosted sub domain in https://neocities.org/ 
The link is : https://steembotcompare.neocities.org/
User can directly start analysis going to this web adress.
Tests in Google Chrome, Opera Browser and FireFox browser are done.
Google Chrome and Opera are working fine but there is screen size problem in FireFox.

### CODE
The programing language is HTML - JavaScript and the single source is the [index.html](https://github.com/firedreamgames/SteemBotCompare/commit/8244d81d145a809d475eff40b93cde463aee87eb) file.

The source is steem.js libraries.
![image.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1514497904/stprkaleay23fwg0vb3o.png)


The script that make the analysis of the steem blockchain is :
*var release = steem.api.streamTransactions('head', function(err, result)* 

The full code is in the GitHub: [index.html](https://github.com/firedreamgames/SteemBotCompare/commit/8244d81d145a809d475eff40b93cde463aee87eb)




