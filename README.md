# dliveProjectData

This data set is for DLive data collected via the earnings API at https://graphigo.prd.dlive.tv June 2020 - February 2021. 

## Table: collections
File: collections.csv.gz. Data was collected 13 times. 

#### collections columns

## Table: users
File: users.csv.gz. There are 119 users in this data set, divided into three main categories:
* Streamers. The far-right extremist streamer category consists of 55 individuals or groups who regularly create English-language content and receive donations on the DLive platform. 
* Mega-Donors. This data set consists of 20 users who have donated in large amounts to the streamers
* People of Interest. We collected data for an additional 44 people classified as "far-right people of interest"

#### users columns

## Table: wallets
File: wallets.csv.gz. We designate a new wallet for each user collection. This is mostly an artifact of early collection when we were capturing wallet data as a standalone item.

#### wallet columns

## Table: transactions
File: transactions.csv.gz. There are 1,048,753 transactions in this data set. There are 6 types of transactions:
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

#### transactions cleaning advisory
Due to a bug in the cloud storage export routine, NULL fields in the original database were converted to ```"N,```. This string should be interpreted as NULL.

## Table: relationships
File: relationships.csv.gz. Describes the follower/following relationships between users.

#### relationships columns

#### relationships cleaning advisory
Due to a bug in the cloud storage export routine, NULL fields in the original database were converted to ```"N,```. This string should be interpreted as NULL.

