# Luck2-2poc description #

## 1 Hardware requirements ##
The recommended requirements is:

1 Processor: CPU with 2 threads or more

2 RAM: 4GB or more

3 Disk space: 10GB - 60GB or more

## 2 Prepare ##

Download the linux wallet from [https://lucknet.club/wallets-luck2/luck2](https://lucknet.club/wallets-luck2/luck2) (md5sum: 94fe585bee2989ea7fa76998d78a1f67) and set it to have executable permissions.

    $chmod +x luck2

## 3 Start the node service ##

With the executable program `luck2`, you can run the backend service and interactive console.

First, create the luck2 data storage directory

    $mkdir ~/luck-data

Start

    $luck2 --datadir=~/luck-data

## 4 Start the luck2 console ##

After you successfully start the node service, you will see luck2.ipc in the data directory.

Start the console

    $luck2 attach ~/luck-data/luck2.ipc

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

## 6 Plotting ##

Before mining, you need to plot hash data to the disk first.

Set plot data directory (According to POC, the directory needs to store a lot of hash data, requiring 10GB-40GB or more hard disk space)

    > miner.setPlotDirectory("<Directory>")
    > true

Start plotting ()

    > miner.startPlot("<Address>",<Nonce>,"<SingleSize>","<Size>")
    > null

Address - is the address used in mining.

Nonce - is the start nonce (uint256), you can set it to 0.

SingleSize - is the size of one single plot file, such as 128MB, 256MB, 512MB etc

Size - is the total size of all the plot files, such as 10GB, 20GB, 25GB etc.

The ploting process may take some time depending on the total size of the plot files, about 1 days/1 TB.

## 7 Mining ##

Set miner

    > miner.setEtherbase("<Miner's address>")
    > true

Start mining

    > miner.start(1)
    > null

Stop mining

    > miner.stop()
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
