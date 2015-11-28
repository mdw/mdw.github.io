---
layout: post
title:  "Emercoin Setup Notes"
date:   2015-11-20 01:47:39
categories: blockchain emercoin debian
gravatar:   "https://en.gravatar.com/userimage/5924047/07f2a056d18fd10a7054b7c4d2e73ed8.jpeg"
excerpt: Quick how-to about setting up Emercoin to run on Debian 8.2 
---

### Notes on emercoin setup on Debian 8.2 x64

Background: I installed this on a [digitalocean](https://digitalocean.com) droplet. They've been rock solid hosting for me, and very affordable. Tell 'em I sent you.

I setup a new droplet and did the usual stuff, including the absolutely required disabling ssh login for root user. I like to run things as separate users, so `adduser emc` came next. As of Debian8 no more editing sudoers, now there's a simple command: `usermod -a -G sudo <user>` 

Next I downloaded [emercoin](http://emercoin.com) from sourceforge - 

    cd /usr/local/src
    wget http://downloads.sourceforge.net/project/emercoin/0.3.4/emercoin-0.3.4-linux.tar.gz
    tar xvf emercoin-0.3.4-linux.tar.gz
    ln -s /usr/local/src/emercoin-0.3.4-linux/bin/64/emercoind /usr/local/bin/emercoind

__emercoind__ is the headless daemon that you want to run, as the GUI wallet you would run on your desktop is _emercoin-qt_. I want to use it as a _systemd service_, so in _/etc/systemd/system/_ I create a [emercoin.service](/data/emercoin.service.txt) file and start the service by typing:

    systemctl enable emercoin.service
    systemctl start emercoin

Note that in our [emercoin.service](/data/emercoin.service.txt) file we're running this as the user _emc_ and they'll need a config file in their `~/.emercoin` directory. This can be very simple, we only need something like this (be sure to put some _rpcuser_ and _rpcpassword_ on first two lines where I'm showing angle brackets):

    rpcuser=<usernamehere>
    rpcpassword=<userpasswordhere>
    rpcport=8775
    rpcallowip=127.0.0.1

    listen=1
    server=1
    maxconnections=80
    reservebalance=5
    gen=0
    daemon=1

    # activate DNS services for 4 TLDs
    emcdns=1
    emcdnsallowed=.coin|.emc|.lib|.bazar
    emcdnsverbose=4

Now check to see that emercoind is running by typing `emercoind getinfo`

Mine shows this:

    {
        "version" : "v0.3.4emc-1-g48d728d-beta",
        "protocolversion" : 60003,
        "walletversion" : 60000,
        "balance" : 0.00000000,
        "newmint" : 0.00000000,
        "stake" : 0.00000000,
        "blocks" : 51987,
        "moneysupply" : 36294315.46409500,
        "connections" : 8,
        "proxy" : "",
        "ip" : "162.243.22.13",
        "difficulty" : 17523505.84215224,
        "testnet" : false,
        "keypoololdest" : 1448052457,
        "keypoolsize" : 101,
        "paytxfee" : 0.01000000,
        "errors" : "WARNING: Checkpoint is too old. Wait for block chain to download, or notify developers of the issue."
}

Note that it is still downloading the blockchain. Currently it is on block 51987, and emercoin blockchain is on 134890 at the time of writing according to this emercoin [blockchain explorer](https://emercoin.mintr.org/) site.

Also note that to resolve your .emc and .coin domain names, the easiest way is to change your machine's DNS settings to point to [opennic's DNS servers](https://opennicproject.org)

Have fun and keep an eye out. If time allows I will write up brief summaries of some of the nice tricks emercoin can do. 
