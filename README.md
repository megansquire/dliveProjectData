# dliveProjectData

This data set is for DLive data collected via the earnings API at https://graphigo.prd.dlive.tv June 2020 - February 2021. 

Please cite as follows:
Megan Squire (2021). Monetizing Propaganda: How Far-right Extremists Earn Money by Video Streaming. In WebSci ’21: 13th International ACM Conference on Web Science in 2021, June 21–25, 2021. ACM, New York, NY, USA, 10 pages. https://arxiv.org/abs/2105.05929

## Table: collections
File: collections.csv.gz. Data was collected 13 times. 

#### collections columns
* collectionID, PK, int, not nullable
* dateOfCollection, datetime, not nullable, default current_timestamp
* notes, varchar(500), nullable

## Table: people
File: people.csv.gz. There are 119 users in this data set, divided into three main categories:
* Streamers. The far-right extremist streamer category consists of 55 individuals or groups who regularly create English-language content and receive donations on the DLive platform. 
* Mega-Donors. This data set consists of 20 users who have donated in large amounts to the streamers
* People of Interest. An additional 44 people classified as "far-right people of interest"

#### people columns
* personID, PK, int, not nullable
* id, varchar(50), nullable
* username, varchar(50), nullable
* displayName, varchar(50), not nullable
* isDeleted, tinyint, not nullable, default 0
* primaryType, enum('streamer','donor','poi'), not nullable
* notes, text 

## Table: peoplePartnerStatus
File: peoplePartnerStatus.csv.gz. Indicates each user's current partner status in the DLive system. New records added for each collection.

#### peoplePartnerStatus columns
* partnerStatusID, PK, int(11), not nullable, auto_increment
* personID, int, not nullable -- FK back to people table
* collectionID, int, not nullable -- FK back to collections table
* partnerStatus, varchar(50), not nullable -- Values: Affiliate, Verified_Partner, None

## Table: relationships
File: relationships-aa.csv.gz (also includes -ab, -ac). Describes the follower/following relationships between users. "Source" is the user doing the following. "Target" is the user being followed.

#### relationships columns
* relationshipID, PK, int, not nullable, auto_increment
* collectionID, int, not nullable -- FK back to collections table
* sourceUserID, varchar(50), not nullable 
* sourceUserName, varchar(50), nullable
* sourceDisplayName, varchar(50), not nullable
* sourcePartnerStatus, varchar(50), nullable
* sourceFollowerCount, int, nullable
* targetUserID, varchar(50), not nullable
* targetUserName, varchar(50), nullable,
* targetDisplayName, varchar(50), not nullable
* targetPartnerStatus, varchar(50), nullable
* targetFollowerCount, int, nullable

#### relationships cleaning advisory
Due to a [bug](https://cloud.google.com/sql/docs/mysql/known-issues) in the cloud storage export routine, NULL fields in the original database were converted to ```"N,```. This string should be interpreted as NULL.

## Table: transactions
File: transactions-aa.csv.gz (also includes -ab, -ac, -ad, -ae). There are 1,048,753 transactions in this data set. There are 6 types of transactions:
* Cash In (count: 28200)
* Cash Out (count: 3261)
* Donation In (count: 965344)
* Donation Out (count: 49448)
* Subscription Income (count: 2497)
* Subscription Paid (count: 3)

For Cash-Out, there are 4 subtypes:
* Add to chest
* CashOut (extract cash)
* User requested refund
* Account suspended

#### transactions columns
* txnID, PK, int, not nullable, auto_increment
* walletID, int, not nullable -- FK back to wallets table
* seq, bigint, not nullable -- every transaction was given a sequence number in the DLive system
* txType, varchar(50), nullable
* createdAt, bigint, nullable -- unix timestamp in ms
* createAtConv, datetime, nullable -- derived field; conversion of unix timestamp to datetime
* description, varchar(100), nullable -- textual description of the transaction
* descDonator, varchar(50), nullable
* descDonatorShort, varchar(100), nullable -- derived field
* descDonatorDisplay, varchar(100), nullable -- derived field
* descQty, bigint, nullable -- the quantity in the transaction, if applicable
* descCurrency, varchar(50), nullable
* descReceiver, varchar(50), nullable
* descReceiverShort, varchar(50), nullable -- derived field
* descReceiverDisplay, varchar(100), nullable -- derived field
* amount, bigint, nullable
* balance, bigint, nullable

#### transactions cleaning advisory
Due to a [bug](https://cloud.google.com/sql/docs/mysql/known-issues) in the cloud storage export routine, NULL fields in the original database were converted to ```"N,```. This string should be interpreted as NULL.

## Table: wallets
File: wallets.csv.gz. We designate a new wallet for each user collection. This is mostly an artifact of early collection when we were capturing wallet data as a standalone item.

#### wallet columns
* walletID, PK, int, not nullable, auto_increment
* personID, int, not nullable -- FK back to people table
* collectionID, int, not nullable -- FK back to collections table
