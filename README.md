# -DigitalOcean-mining
mining on  DigitalOcean

XMRig is mining software codded in C++ language.
It’s an open-source software (has a dev fee of 1%) and available to download from official github repository.
We’ll be using an Ubuntu 20.04 server for this tutorial.
If you’re on Ubuntu 20.04 desktop, hit + keys to launch CLI.
If you’re connecting to a remote Ubuntu 20.04 server from Windows, use Putty to connect over SSH. Make sure to login with root user account.

#  Prepare Ubuntu 20.04 to Install XMRig CPU Miner 

Before we start installing XMRig on our Ubuntu 20.04 machine, we need to do some initial maintenance and install some dependencies.
So, log in to your machine and execute following commands to update apt cache.

$ apt update

$ apt upgrade

 It can take a minute or two. Once that’s done, let’s do some cleanup, 
 
$ apt autoremove
 
  Then a reboot, 
  
$ reboot
 
  Log in to your server again when it comes back online. Now we can install the XMRig dependencies with following command. 
  
$ apt-get install git build-essential cmake automake libtool autoconf

 Let it complete and then we’re ready to install XMRig on Ubuntu 20.04. 
 
# Install XMRig CPU Miner on Ubuntu 20.04 

We will be fetching the miner directly from the official Github repository. We can use git clone command for that. Let’s do it,

$ git clone https://github.com/xmrig/xmrig.git

Create the working directory build and then navigate to the scripts directory.

$ mkdir xmrig/build && cd xmrig/scripts

Run the installation script and the navigate to build directory

$ ./build_deps.sh && cd ../build

Install XMRig on Ubuntu 20.04

$ cmake .. -DXMRIG_DEPS=scripts/deps
make -j$(nproc)

Two commands above will take bit longer to process. You are ready to mine Monero on Ubuntu 20.04 once its complete.

# Start mining Monero with XMRig CPU Miner on Ubuntu 20.04 
 
If you were able to complete the above instructions successfully, you’re now ready to mine XMR on your Ubuntu 20.04 or Ubuntu 18.04 machine.
There are two methods you can use the miner.
The first method is by,


$ /root/xmrig/build/./xmrig -a cryptonight -o stratum+tcp://pool.supportxmr.com:5555 -u 47QSLUR7ba7bRmsDdb3czPazQTqwyzTxn3WTNd32qoSn1LNDtsmwsx98q49DdKsxc69b9D3EYDgZZQJ9csDoX2kkFeZgbp8 -p MinerIdentifier:Email -t 0

This will mine Monero on supportxmr.com with 0 CPU. Change your MoneroAddress, MinerIdentifier, Email and the number of treads with the -t vaule towards the end.

The second and the preferred method is by,

Using JSON config file…

In this method, we’ll store miner config in a json file. Let’s create it in the build directory,


$ nano /root/xmrig/build/config.json

Now use the https://xmrig.com/wizard to generate your XMRig miner configuration.

Paste the output from wizard to the config.json file. It should look something like this,

{
    "autosave": true,
    "cpu": true,
    "opencl": false,
    "cuda": false,
    "pools": [
        {
            "url": "pool.supportxmr.com:443",
            "user": "47QSLUR7ba7bRmsDdb3czPazQTqwyzTxn3WTNd32qoSn1LNDtsmwsx98q49DdKsxc69b9D3EYDgZZQJ9csDoX2kkFeZgbp8",
            "pass": "test",
            "keepalive": true,
            "tls": true
        }
    ]
}

Now close the file by hitting "CTRL+X" Following command will launch the miner and start mining Monero on Ubuntu 20.04.

$ /root/xmrig/build/./xmrig



# Happy mining!!
