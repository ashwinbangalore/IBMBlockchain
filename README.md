
<img src="https://farm5.staticflickr.com/4526/38118284672_388e43fc4c_z.jpg" width="640" height="275" alt="IBM Blockchain">

<a href="https://github.com/LennartFr/Blockchain-at-Galvanize/blob/master/README.md"><img src="https://farm5.staticflickr.com/4477/37819497381_afe8896658_o.png" width="773" height="134"></a>

http://bit.ly/2h3F0aq

# Workshop: Introduction to writing Blockchain applications
## The workshop materials are all out on: ibm.biz/blockchaingalvanize

# Housekeeping info:

### Wifi at SouthBay SSID/pass = tbd
Your instructor: Lennart alf@us.ibm.com, Developer Advocate at IBM, focusing on Blockchain, Fintech and Watson.

Marek Sadowski, Syed Zaidi. Maya Reyes, Juanita Dion.

## Assumption: you have brought your laptop and you know enough about Blockchain to want to write Blockchain apps. 

# Agenda
~~~
6:00: Sign-in, mingle, food, welcome, form teams 
6:20: Lennart: Introduction to IBM Blockchain and Hyperledger  
6:40: Coding starts.
      Lab 1: Let's run our first application in Hyperledger Fabric
      Lab 2: Let's write an app with the Hyperledger Composer
      Lab 3: A full app, Decentralized Energy with Hyperledger Composer
8:15: Coding ends.
      Where do we go from here? 
      Developer Journeys for Blockchain
      Q1 2018: Advanced Blockchain, a Hands-on Workshop.
8:30: Event ends   
~~~ 
# Let's get started, introduction and documentation

## How did it all start?

October 2008 It all started with Satoshi Nakamoto and his paper [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) which addressed a key problem in electronic commerce:

<img src="https://farm5.staticflickr.com/4505/24079519258_ab8a80f7ed_o.png" width="769" height="229" alt="Double Spending">

**In this workshop we will use the Hyperledger implementation of Blockchain : http://hyperledger.org/**

Hyperledger, an open source collaborative effort to advance cross-industry blockchain technologies, 
is hosted by The Linux Foundation®. 

Deployed in Docker images.

1. A blockchain emulates a “trusted” computing service through a distributed protocol, 
   run by nodes connected over the Internet. 

2. The service represents or creates an asset, in which all nodes have some stake.

3. The nodes share the common goal of running the service but do not necessarily 
   trust each other for more. 

....

5. On the other hand, blockchains in the “permissioned” model control who participates in validation and
   in the protocol; these nodes typically have established identities and form a consortium

Consensus protocol is pluggable, currently an implementation of Byzantine fault-tolerant con-
sensus using the PBFT protocol.

Source: https://www.zurich.ibm.com/dccl/papers/cachin_dccl.pdf


<img src="https://farm5.staticflickr.com/4494/37926120211_b7dddb090d_o.png" width="682" height="423" alt="Hyperledger Services">

### Hyperledger Composer source code on GitHub https://github.com/hyperledger/composer
Hyperledger Composer is an application development framework which simplifies and expedites the creation of Hyperledger fabric blockchain applications.

### Hyperledger Fabric source code on Github https://github.com/hyperledger/fabric

Hyperledger Fabric is a platform for distributed ledger solutions, underpinned by 
a modular architecture delivering high degrees of confidentiality, resiliency, 
flexibility and scalability. It is designed to support pluggable implementations 
of different components, and accommodate the complexity and intricacies that exist 
across the economic ecosystem.

### [The .bna file](https://hyperledger.github.io/composer/reference/commands.html)
A Business Network Archive (BNA) file is exported by the Hyperledger Composer with 
the extension of .bna, and contains the definitions all the definitions for a Business Network. 
It is deployed in a Hyper Ledger Fabric. 
 
<img src="https://farm5.staticflickr.com/4511/37561438920_efe78c324b_o.png" width="1169" height="199" alt="blockchain-banner2">


[IBM Blockchain 101: Quick-start guide for developers](IBM%20Blockchain%20101.md)


## Prerequisites: 
http://hyperledger-fabric.readthedocs.io/en/latest/prereqs.html

We will be developing on our laptops. MacOS, Ubuntu or Windows.

# Lab 1: Let's run our first application in Hyperledger Fabric 
Original instructions: http://hyperledger-fabric.readthedocs.io/en/latest/write_first_app.html

## Step 1 First, remove the containers, next, delete the chaincode image:

    1 docker rm -f $(docker ps -aq)
    2 docker rmi dev-peer0.org1.example.com-fabcar-1.0  //delete chaincode image
    
## Step 2 Navigate to a directory where you want the samples downloaded to, and issue these commands:

    1 git clone https://github.com/hyperledger/fabric-samples.git
    2 cd fabric-samples/fabcar
    3 See what's inside the directory: ls
    4 You should see the following: chaincode , invoke.js , network , package.json , query.js , 
      startFabric.sh
    5 Start the fabric: ./startFabric.sh
   
   Output:
   
  <i>  Creating network "net_basic" with the default driver
    Creating couchdb ... 
    
    Creating ca.example.com ...
    
      CA: Certificate Authority https://hyperledger-fabric-ca.readthedocs.io/en/latest/ 
         Comment: It provides features such as:
         1. Issues certificates to other network participants to enroll in the network,
	       or connects to LDAP as the user registry
         2. issuance of Enrollment Certificates (ECerts)
         3. certificate renewal and revocation
	     
    Creating orderer.example.com ...
    
        Comment: The Hyperledger fabric ordering service is intended to provide an atomic broadcast 
        ordering service for consumption by the peers. This means that many clients may 
	submit messages for ordering, and all clients are delivered the same series of 
	ordered batches in response.
    
    Creating ca.example.com
    
    Creating orderer.example.com
    
    Creating couchdb ... done
       Comment: Transactions are collected into blocks/batches on the Ordering Service.
       The  blocks are stored locally to disk on every Ordering Service node 
       along with a LevelDB or CouchDB index to these blocks by number. 
       The blocks are delivered via RPC to committing peers. 
       The peers store them locally, and maintain a LevelDB (or CouchDB)based block index. 
       http://bit.ly/2zORhrC
    
    Creating peer0.org1.example.com ...
       Comment: A Peer is a node that validates and commits transactions and maintains the state and a copy 
       of the ledger. 

       Every peer stores the data of the blockchain in its container. 
       In a production envirement this container has a volume (mounted folder) to a real hard drive, NAS, SAN 
       or any other storage that you may use. Otherwise if the container is stopped all the data that was in the 
       container will be gone. 
       
       Every peer stores exactly the same data. So if a blockchain is 10Gb and you have 5 peers 
       then 50Gb will be needed to store 5 separate files from every peer and every file is 10Gb.

       Creating peer0.org1.example.com ... 
       done
       
  <img src="https://farm5.staticflickr.com/4458/37771305586_6bf75bc2af_o.png" width="853" height="482" alt="hyperledger architecture">

  </i>
   
    6 Install the SDK Node modules: npm install  
    7 node query.js
       
  output;
   Arnes-MBP:fabcar arnelennartfrantzell
   $ node query.js
   Create a client and set the wallet location
   Set wallet path, and associate user  PeerAdmin  with application
   Check user is enrolled, and set a query URL in the network
   Make query
   Assigning transaction_id:  9367267e0e9c66cba821eb79500ffee6f004ced6f53bc01ddf280b00e2a8cb10
   returned from query
   Query result count =  1
Response is  
[{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},

 {"Key":"CAR1", "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},

 {"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},
 
 {"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},
 
 {"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},
 
 {"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},
 
 {"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},
 
 {"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},
 
 {"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},
 
 {"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]
 
  
## Step 3 Now let's add a new car and update the Blockchain.

1 Open the Invoke.js program, locate the request function and change the args section like this, 
using your own name and args:

~~~
var request = {
        targets: targets,
        chaincodeId: options.chaincode_id,
        fcn: 'createCar',
        args: ['CAR10', 'Chevy', 'Volt', 'Red', 'Lennart'],
        chainId: options.channel_id,
        txId: tx_id

2 Save the file and invoke it like this: node invoke.js. 
3 Followed by: node query.js
You should see the new car appear, stored in the blockchain.
~~~

## Step 4 Now let's change car ownership

1 Change the Invoke.js program as shown below:

~~~
// createCar - requires 5 args, ex: args: ['CAR11', 'Honda', 'Accord', 'Black', 'Tom'],
    // changeCarOwner - requires 2 args , ex: args: ['CAR10', 'Barry'],
    // send proposal to endorser
    var request = {
        targets: targets,
        chaincodeId: options.chaincode_id,
     // fcn: 'createCar',
        fcn: 'changeCarOwner',
     // args: ['CAR10', 'Chevy', 'Volt', 'Red', 'Lennart'],
        args: ['CAR10', 'Syed'],
        chainId: options.channel_id,
        txId: tx_id
    };
~~~

2 Again, enter node query.js.

You will see that the new owner is now Syed.

This concludes Lab 1.

# Lab 2: Let's write an app with the Hyperledger Composer!
<img src="https://farm5.staticflickr.com/4445/37751618086_06402e4b2e_b.jpg" width="383" height="266" alt="Composer Playground">

[Playground Tutorial](https://hyperledger.github.io/composer/tutorials/playground-guide.html)

## Run Hyperledger Composer in your browser https://hyperledger.github.io/composer/

## [Instructions (open in parallel window): Composer Playground and the Perishable Goods Network]

(https://github.com/LennartFr/Blockchain-at-Galvanize/blob/master/Hyperledger%20Composer%20Perishable%20Food%20Network%203.pdf)

This concludes the second lab centered arund the Composer Playground. 

# Lab 3: Decentralized Energy with Hyperledger composer 

This third lab, a Developer Journey written by Raheel Zubairy of IBM, describes a complete blockchain application with a decentralized energy network with a working user interface.

https://developer.ibm.com/code/journey/decentralized-energy-hyperledger-composer/

Lab Instrructions: https://github.com/IBM/Decentralized-Energy-Composer?cm_sp=IBMCode-_-decentralized-energy-hyperledger-composer-_-Get-the-Code

## This concludes the lab portion of this workshop

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">

# Overview of the Hyperledger architecture

### The flow with one SDK

<img src="https://farm5.staticflickr.com/4479/37162470013_1309212044_b.jpg" width="1024" height="513" alt="Hyperledger Architecture">

### The flow with two and more SDKs

<img src="https://farm5.staticflickr.com/4506/37882671951_5f4f08348a_o.png" width="1142" height="635" alt="Hyper Ivan 2">

### The Blockchain and State database.

<img src="https://github.com/LennartFr/Blockchain-at-Galvanize/blob/master/Hyperledger%20LevelDB.PNG">

### Ordering service

<img src="https://www.ibm.com/developerworks/cloud/library/cl-top-technical-advantages-of-hyperledger-fabric-for-blockchain-networks/fig1.png">

### Blockchain Ledger

<img src="https://farm5.staticflickr.com/4496/37833953496_fa03154139_o.png" width="837" height="421" alt="Ivan Blockchain">

# Hyperledger Fabric and its docker images 

<img src="https://farm5.staticflickr.com/4506/23967210328_2ab9949bdb_o.png" width="701" height="812" alt="hyper docker">

<img src="https://farm5.staticflickr.com/4503/37148677233_71edc5a37b_o.png" width="1041" height="53" alt="blueband">


# Where do we go from here?

<img src="https://farm5.staticflickr.com/4338/36822231841_bc13a7147a_z.jpg" width="640" height="164" alt="IBMBlockchain1">

[Blockchain for Dummies](https://public.dhe.ibm.com/common/ssi/ecm/xi/en/xim12354usen/XIM12354USEN.PDF)


## IBM has a series of Developer Journeys covering various aspects of Blockchain, with more being added regularly. 

* https://developer.ibm.com/code/journey/build-your-first-blockchain-application/
* https://developer.ibm.com/code/journey/create-and-execute-blockchain-smart-contracts/
* https://developer.ibm.com/code/journey/implement-fda-food-supplier-verification-program-on-hyperledger-composer/
* https://developer.ibm.com/code/journey/build-a-blockchain-network/
* https://developer.ibm.com/code/journey/decentralized-energy-hyperledger-composer/
* https://developer.ibm.com/code/journey/run-blockchain-technology-on-a-linux-mainframe/
* https://developer.ibm.com/code/journey/create-a-to-do-list-app-using-blockchain/
* https://developer.ibm.com/code/journey/deploy-an-asset-transfer-app-using-blockchain/

# https://www.hyperledger.org/community

## Blockchain in the IBM Cloud: https://console.bluemix.net/catalog/services/blockchain/ 

<img src="http://34b70.http.dal05.cdn.softlayer.net/broker-static/v1-ga1/img4.png">

** Initiate a new blockchain network including setting democratic network policies and inviting new members to join.
** Join a network, as a new member, based on an invite from the network initiator.

* Use Issues to log suggestions to this workshop.
https://github.com/LennartFr/Blockchain-at-Galvanize/issues/1


# Appendix

## Bonus Lab : Let's bring up the Hyperledger Fabric!
Instructions below from thess URLs: 
* http://hyperledger-fabric.readthedocs.io/en/latest/build_network.html 
* http://hyperledger-fabric.readthedocs.io/en/latest/samples.html
* http://hyperledger-fabric.readthedocs.io/en/latest/getting_started.html

### Step 1
Only if necessary, execute the following three commands to remove existing Docker instances.
   * docker kill $(docker ps -q)
   * docker rm $(docker ps -aq)
   * docker rmi $(docker images dev-* -q) 
### Step 2   
    Instructions below come from the following URL: http://hyperledger-fabric.readthedocs.io/en/latest/samples.html  
    From a terminal window on your laptop, execute the following commands:
   * git clone https://github.com/hyperledger/fabric-samples.git into a directory on your laptop
   From that directory on your laptop (see above) invoke:
   * curl -sSL https://goo.gl/Q3YRTi | bash   
   * export PATH=<path to download location>/bin:$PATH  
  
### Step 3 
   * Instructions below come from the following URL:  
      http://hyperledger-fabric.readthedocs.io/en/latest/build_network.html
      
   Bring up the Hyperledger Fabric: 
   * cd first-network
   * ./byfn.sh -m generate
   * ./byfn.sh -m up. //See full output from command on this link http://bit.ly/2yyTeIj
   * After checking the output, remember to run ./byfn.sh -m down.
   
 ### Step 4 (optional) Configurate your Hyperledger Fabric instance.  
 http://hyperledger-fabric.readthedocs.io/en/latest/build_network.html



## Deploy bna file on hyperledger fabric
https://hyperledger.github.io/composer/business-network/bnd-deploy.html
``~
Arnes-MBP:bnafile arnelennartfrantzell$ composer network deploy -p hlfv1 -a my-basic-sample.bna -i PeerAdmin -s randomString -A admin -S
Deploying business network from archive: my-basic-sample.bna
Business network definition:
	Identifier: my-basic-sample@0.1.10
	Description: The Composer basic sample network

✔ Deploying business network definition. This may take a minute...

Command succeeded
~~~

## ping application on hyperledger composer

Arnes-MBP:bnafile arnelennartfrantzell$ composer network ping -n my-basic-sample -p hlfv1 -i admin -s adminpw
The connection to the network was successfully tested: my-basic-sample
	version: 0.14.1
	participant: org.hyperledger.composer.system.NetworkAdmin#admin

Command succeeded

~~~

