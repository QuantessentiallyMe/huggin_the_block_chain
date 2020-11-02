# How To: Use Mine
Here I will be explaining how to start and interact with my PoA Blockchain Network called "Futurebank".

## Pre-Work
Be sure to have everything installed...
***1. Installing MyCrypto:***
  - MyCrypto is a free, open-source, client-side interface that allows you to interact directly with the blockchain. You will find MyCrypto Desktop App here: [MyCrypto](https://download.mycrypto.com/).

***2. Installing Go Etheruem Tools:***
  - Go Ethereum is one of the three original implementations of the Ethereum protocol and is written in Go. You will use Go Ethereum Tools to create the blockchain from the genesis block to mining tokens and making transactions.
    - Navigate to the download page here: [Go Ethereum](https://geth.ethereum.org/downloads/). You want the most recent "Geth & Tools" and if you are using Windows you should choose between 32 and 64 bit depending on what you are running. To figure out which you are running check this out: [Which Windows?](https://support.microsoft.com/en-us/windows/which-version-of-windows-operating-system-am-i-running-628bec99-476a-2c13-5296-9dd081cdd808).
    - After downloading everything you will find a file named "geth-all-tools....", decompress this archive in a location of your preference and rename it as something memorable. I call my folder "Blockchain-Tools". I believe it is pretty straightforward to know what is going on in there. Put it in a location that is easily accessible through the terminal. This instructional will basically be completely done in the terminal. At this point you have completed the instillation process and may proceed.

## The Good Stuff
Now that we have all of the necessary tools, we can get into the blockchain.

1. At this point you should have your own "Blockchain-Tools" folder. Here in the repo there is an x_node1 folder, an x_node2 folder and a futurebank.json file. All of these files and folders need to be located in your "Blockchain-Tools" folder or whatever you decided to call it.

2. Now that you have all the files and folders that are needed you will need to ***open two DIFFERENT terminal windows*** there will be one window for each respective node. You will need to first get to your "Blockchain-Tools" directory in each respective terminal and then run the code below:
```
(Terminal Window 1)
x_node1:
./geth --datadir x_node1 --unlock c65c504802BC4F1B9d7670ff2Af1550Dd0C1f73E --mine --rpc --allow-insecure-unlock
```
```
(Terminal Window 2)
x_node2:
./geth --datadir x_node2 --unlock 0dC59017d8160A8e035F1763dAfbc214C2f0f3fD --mine --port 30304 --bootnodes enode://15f948d7b9ac65b461f83fb5252495876d8833cecdea5fc149eaffae083422d7aae35c760872e80cade6db2570e0f479266d782f678530b7196a331c72347253@127.0.0.1:30303 --ipcdisable --allow-insecure-unlock
```
If everything is running properly your screen should look like this.
![node1 start](/Screenshots/x_node1_startup.png)
Above is an example of starting up x_node1.

![node2 start](/Screenshots/x_node2_startup.png)
Above is an example of starting up x_node2.

After a while, once they really start going and mining, the two windows side by side should look like this:
![nodes together](/Screenshots/x_node1_and_x_node2_running.png)
Notice all of the mining and actually pictures of hammers and chains for example. All computers do not specifically show these images but this helps to notice that things are working properly. ***I also have a video located in the screenshots folder called two_nodes_running.mov where you can see them in action to get an understanding***

### Testing/ Making Transactions
At this point we have the actual blockchain running. It is now time to send money between our peers within our network. I will illustrate here how to connect the custom network to MyCrypto and then send transactions. Here I will be sending between the nodes, but all you would have to do is connect your own personal wallet to the custom network as opposed to when I connect to x_node1 with the keystore in my example and use that wallet in MyCrypto.

***At this point I actually have some videos located in the screenshots folder. For these next few steps you would watch "connecting_node_to_mycrypto.mov."***

1. Click "Change Network" at the bottom left after opening MyCrypto.
![select change](/Screenshots/change_network_select.png)

2. Scroll all the way down, focusing on the right scroll window of the app and once at the bottom you will find "Add Custom Node". Click on "Add Custom Node".
![add custom node](/Screenshots/add_custom_node.png)

3. Here you will add the custom network information. The Node Name and Network Name will both be called Futurebank. The Network will be assigned to Custom. The currency will be ETH. The Chain ID will be 303030. The URL will be the default URL so it will route to your local network:
http://127.0.0.1:8545. You will then select "Save & Use Custom Node" (***Again this can all be found in the video***)
![add custom info](/Screenshots/add_custom_network_info.png)


4. Now the network is connected and can be used. I will now test it by sending money between accounts. This would be the point where you simply open your own wallet. You are done. ***This video can be found in the screenshots folder under "connecting_node_keystore_to_wallet.mov***. Back on the main page we will select "Keystore File" at the bottom middle in the "How would you like to access your wallet?" section. It would also be great if you made your own node, at this point you could follow these steps and add your own personal keystore.
![select how](/Screenshots/how_would_you_like_to_access.png)

5. The next screen will allow you to "Unlock your Keystore File". Here you will need the keystore file for your node, I am using x_node1, and to remember the password you initially created for your node. You will select "SELECT WALLET FILE" and then go to the keystore file. You will select that file and then in the password section type in your node password.
![select wallet file](/Screenshots/select_wallet_file.png)

6. Your account wallet should now be open inside of MyCrypto. At this point you can go to the "to address" section, paste the public address for whoever you want and send money. I am inside of the wallet for x_node1 and will be sending test money to x_node2. ***I have a video of all of this and how to check if it sent in the screenshots section under send_money_to_node_2.mov***
![send address example](/Screenshots/sending_money_address_ex.png)
![confirm transaction](/Screenshots/confirm_transaction.png)
After confirming the transaction you can then check the status to see how it went. A green banner will appear at the bottom of your wallet screen where you can click "Check TX Status" it will log you out, but you can follow the transaction to see if it was successful
![check status](/Screenshots/check_status.png)
Finally, if everything was successful you should see this.
![succesful transaction](/Screenshots/successful_transaction.png)
DONE!!



