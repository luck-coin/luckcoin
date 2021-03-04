# How to mine -- base on linux #

This article will cover following:

1) Hardware requirements.

2) Prepare.

3) Start the node service

4) Start the luck console

5) Accounts management

6) Mining

7) Send transactions

## 1 Hardware requirements ##
With the current scale of the mainnet, the recommended requirements is:

1 Processor: CPU with 2 threads or more

2 RAM: 4GB or more

3 Disk space: 100G


## 2 Prepare ##

Download the linux wallet from the website and Set it to have executable permissions.

    $chmod +x luck


## 3 Start the node service ##

With the executable program `luck`, you can run the backend service and interactive console.

First, create the luck data storage directory

    $mkdir ~/luck-data

Start

    $luck --datadir=~/luck-data


## 4 Start the luck console ##

After you successfully start the node service, you will see luck.ipc in the data directory.

Start the console

    $luck attach ~/luck-data/luck.ipc

In which you can run complex Javascript interactive commands, the command to exit the console is

    > exit

## 5 Accounts management ##

Create account

    > personal.newAccount("<unlock password>")
    > "<address>"
    
View all accounts

    > fort.accounts
    > ["<address>", "<address>"]

Unlock account

	> personal.unlockAccount("<address>", "<unlock password>")
	> true

Get balance
    
    > fort.getBalance("<address>")
    > <balance>

## 6 Mining ##

Set miner

    > miner.setEtherbase("<Miner's address>")
    > true

Start mining

    > miner.start(1)
    > null

Stop mining

    > miner.stop(1)
    > null

Get the current height

    > fort.blockNumber
    > <Number>

Get Block info

    > fort.getBlock(<Number>)
    > {
    >   <block details>
    > }

Get mining state

    > fort.mining
    > <true or false>

## 7 Send transactions ##

Send Transaction

	> fort.sendTransaction({"from":"<Sender Address>","to":"<Receiver Address>","value":"<Value>"})
	> "<Transaction Hash>"

Get status of a transaction

    > fort.getTransaction("<Transaction Hash>")
    > {
    >    <Transaction Details>
    > }

