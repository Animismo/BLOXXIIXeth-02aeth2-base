# Beaconnode & validator using Docker

####  [Official **PrysmaticLabs Docs**](https://docs.prylabs.network/docs/getting-started/)\*\*\*\*

#### Step 0. 

[Install docker ](https://docs.docker.com/docker-for-mac/install/)

#### **Step 1.**

Check if **Docker** is installed through the terminal.   
This can be done by pressing `CMD+Space` and searching for **Terminal**.

Run `docker -v` .  
If the output returns the docker version, Docker is installed correctly.

![](../../../.gitbook/assets/image%20%2818%29.png)

\*\*\*\*

#### **Step 2.**

**Download and install latest beaconchain updates**

`docker pull gcr.io/prysmaticlabs/prysm/beacon-chain:latest`

**Download and install latest validator updates**

`docker pull gcr.io/prysmaticlabs/prysm/validator:latest`

![](../../../.gitbook/assets/image%20%282%29.png)

#### **Create a docker network**

`docker network create --attachable medalla`

#### **Start the beaconnode**

`docker run -ti --name beacon-chain --network medalla -v $HOME/prysm:/data  -p 12000:12000/udp -p 13000:13000 gcr.io/prysmaticlabs/prysm/beacon-chain:latest --datadir=/data --rpc-host=0.0.0.0`

![](../../../.gitbook/assets/image%20%287%29.png)

The directory `$HOME/prysm` contains all the beaconchain data and can be accessed through **Finder.**

![](../../../.gitbook/assets/image%20%2820%29.png)

**Wait** for the beaconnode to be in sync with the blockchain.   
This may take a few hours and you will see the following message:

`INFO initial-sync: Synced up to slot XXXXX`

![](../../../.gitbook/assets/image%20%281%29.png)

\*\*\*\*

#### **Step 3.**

**Create ETH2 Keys**

Open a **new Terminal** window and run:

`docker run -it -v $HOME/eth2validator:/data gcr.io/prysmaticlabs/prysm/validator:latest accounts create --keystore-path=/data --password=yourPassword`

![](../../../.gitbook/assets/image.png)

{% hint style="info" %}
The created Keys are now located in **$HOME/eth2validator** 
{% endhint %}

**Copy the Raw Transaction Data** and go to the [participation page](https://prylabs.net/participate).  
Some of the instructions on the participation page will be ignored because they are not required anymore. 

Follow the steps below to get Goerli ETH and to deposit them ****to activate your validator. If you cannot get any Goerli ETH through the participation page, join the [Prysm Discord](https://discord.gg/wJW7Rjk) channel.

![](../../../.gitbook/assets/image%20%286%29%20%283%29.png)

#### **Step 4.**

**Start the validator**

Open a **new Terminal** window and run:

`docker run -ti --name validator --network medalla -v $HOME/eth2validator:/data gcr.io/prysmaticlabs/prysm/validator:latest --keystore-path=/data --datadir=/data --password=yourPassword --beacon-rpc-provider=beacon-chain:4000`

#### **Step 5.**

Track your validator performance on [beaconcha.in](https://beaconcha.in/dashboard?validators=) with your public key \(orange\).   
Once the blockchain recognises the deposit, the [beaoncha.in](https://beaconcha.in/) explorer will allow you to track the validator more accurately.

Wait for the inclusionSlot \(red\) to be reached. Once the blockchain has processed this slot, you will be staking! The Slot number can be tracked [here](https://beaconcha.in/blocks).

![](../../../.gitbook/assets/image%20%2835%29.png)

\*\*\*\*

#### **Running multiple validators** 

Repeat **Step 3.** and **create more keys** into the same directory.   
**Use the same password for all keys.**

Copy the **Raw Transaction Data** for each validator, re-do the process on the [participation page](https://prylabs.net/participate) and deposit for each of them.

Once the system has received all deposits, you can just start a single validator "window", and it will use **all** of the created keys \(=multiple validators\).

{% hint style="success" %}
For further assistance, please join the Prysmatic Labs Discord [channel](https://discord.gg/wJW7Rjk).
{% endhint %}



