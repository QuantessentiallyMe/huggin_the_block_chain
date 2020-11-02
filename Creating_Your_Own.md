# How To: Create
Here I will be trying my best to give a thorough step by step setup of your very own blockchain network using Puppeth, Geth, and MyCrypto. I have also attached videos to help along with pictures in the screenshots folder.

## Pre-Work
Be sure to have everything installed...
***1. Installing MyCrypto:***
  - MyCrypto is a free, open-source, client-side interface that allows you to interact directly with the blockchain. You will find MyCrypto Desktop App here: [MyCrypto](https://download.mycrypto.com/).

***2. Installing Go Etheruem Tools:***
  - Go Ethereum is one of the three original implementations of the Ethereum protocol and is written in Go. You will use Go Ethereum Tools to create the blockchain from the genesis block to mining tokens and making transactions.
    - Navigate to the download page here: [Go Ethereum](https://geth.ethereum.org/downloads/). You want the most recent "Geth & Tools" and if you are using Windows you should choose between 32 and 64 bit depending on what you are running. To figure out which you are running check this out: [Which Windows?](https://support.microsoft.com/en-us/windows/which-version-of-windows-operating-system-am-i-running-628bec99-476a-2c13-5296-9dd081cdd808).
    - After downloading everything you will find a file named "geth-all-tools....", decompress this archive in a location of your preference and rename it as something memorable. I call my folder "Blockchain-Tools". I believe it is pretty straightforward to know what is going on in there. Put it in a location that is easily accessible through the terminal. This instructional will basically be completely done in the terminal. At this point you have completed the instillation process and may proceed.

## The Good Stuff
Now that you are sure you have everything installed here I will try my best to give a through step by step setup of a PoA (Proof of Authority) consensus blockchain network.

1. PoA requires pre-approval so it its typical the algorithm used for private blockchain networks. Because of this, we will have to generate our nodes first. These nodes we will then make the "sealers" which will mean they authorize/approve transactions (they seal blocks). To create these nodes we will head over to our "Blockchain-Tools" folder via the terminal and run:
```
(Code for node1, here I use "node1" but you can name it whatever you would like.)
./geth account new --datadir node1 
```
![example node1](/Screenshots/ex_node_1_picture.jpg)
In the above example one can see the code ran with ex_node1 as the name for said "node1". There will be a request for a password, you must remember this because this will be the only password to decrypt the node. You will then receive the Public Address for the node and a path to a secret key file. Keep this information they will be needed later.

```
(Code for node2, here I used "node2" but again you can name it whatever you would like.)
./geth account new --datadir node2
```
![example node2](/Screenshots/ex_node_2_picture.png)
This is an example for "node2". Here again remember, one needs to take note of his/her password, public address, and the secret key file path.

2. We now have two nodes ready to be sealers. We can move forward to developing the network. Now with puppeth, inside of our Go Ethereum Tools folder I call "Blockchain-Tools" (run: ***open puppeth***), we will be creating a genesis block. A genesis block is the first step towards creating your very own blockchain. It is the first block ever mined, forms the foundation of the entire chain, and is the prototype of all other blocks.
  - After running Puppeth you then name your network. Below one will find a screenshot example using the network name "chrisbank". 
![name network](/Screenshots/name_network.png)

3. Still inside of puppeth and generating our genesis block, we will select option ***2. Configure new genesis*** for the response to, "What would you like to do? (default = stats).
![choose to create](/Screenshots/choose_to_create.png)

4. We then select the option ***1. Create new genesis from scratch*** for the response to, "What would you like to do? (default = create).
![create new genesis](/Screenshots/choose_to_create_new_genesis.png)

5. Now you get to decide if you will use the PoW (Proof of Work) algorithm or the PoA (Proof of Authority) algorithm to seal blocks. We will be creating a PoA network so select ***2. Clique - proof-of-authority*** in response to, "What consenus engine to use? (default = clique).
![select algo](/Screenshots/select_algo.png)

6. For "how many seconds should blocks take", I just used the default of 15. You can pass the argument of 15 and click enter.

7. You will now paste the two public addresses for the two nodes we created earlier in step 1. These two nodes will be given authority to seal blocks. (Remember I said to take note.) You will paste the entire public address sans the 0x. (Disregard the discrepencies in these example addresses.)
![paste sealers](/Screenshots/allow_sealers.png)

8. We will then paste the account public addresses again to be pre-funded. There are no block rewards in PoA, so we need to pre-fund. (I suggest pasting them in the same order as you did in step 7.)
![fund accounts](/Screenshots/fund_accounts.png)

9. "Should the precompile-addresses (blah blah)...."? For this I suggest saying no.

10. You will now specify your chain/network ID. This is important and needs to be taken note of somewhere. Decide your own chain ID and record it. Here I am using 31313 as an example. 
![network id](/Screenshots/chain_id.png)

11. You should now be back at the main window asking what you would like to do. Get excited, you are very close to running your own blockchain network. Here you will now select ***2. Manage existing genesis.***
![manage genesis](/Screenshots/manage_existing_genesis.png)

12. You will now export your genesis configuration. Select ***2. Export genesis configurations.*** I suggest exporting it into this same folder, this folder I am calling "Blockchain-Tools". Two of the files will fail to create and this is fine we only care about the file that is your network name dot json. (networkname.json).
![export genesis](/Screenshots/export_genesis.png)

You can see the error as well as the directory request below.
![save with error](/Screenshots/save_with_error.png)

13. We now have the genesis block created. We now need to initialize everything. We will first be initializing each node using geth and the genesis json file. These need to be in the same directory. This code below will consist of the name you decided for your nodes, here we will have node1 for the first node, and node2 for the second node, and the json file that is simply the name you decided for your network and dot json. (your_network_decided_name.json) 

```
./geth init networkname.json --datadir node1

./geth init networkname.json --datadir node2
```
![initialize node 1](/Screenshots/initialize_node1.png)
Above I am initializing ex_node1 my "node1" with my chrisbank.json file for my "networkname.json" file.

![initilize node 2](/Screenshots/initialize_node2.png)
The same is occurring above for node2. 

14. Now we can use our nodes to begin mining blocks. ***YOU MUST RUN THE NODES IN SEPARATE TERMINAL WINDOWS***. We will now run our nodes. You will open your separate terminal windows and run these commands. Remember to first go to your "Blockchain-Tools" directory in each terminal before moving forward.
```
(Terminal Window 1)
./geth --datadir node1 --unlock NODE1_PUBLIC_ADDRESS --mine --rpc --allow-insecure-unlock
```
***TWO IMPORTANT THINGS: Type your password and hit enter - even if you can't see it visually. If you don't want to, make a text file all in this same folder and call it pw.txt for example. Add an additional flag to the code above, --password and type pw.txt. Here is an example:***
```
./geth --datadir node1 --unlock NODE1_PUBLIC_ADDRESS --mine --rpc --password pw.txt --allow-insecure-unlock
```

***Also once this node begins to run, quickly look for when it says "Started P2P networking" as found in the picture below. You will want to then copy the information that starts with "self=" with the self being green. You specifically want the enode information. This enode information will be tagged at the end of your node2 as its bootnode. Node2 will also have its own enode P2P that you should take note of as well.***
![node p2p](/Screenshots/node1_p2p.png)

Now I will give the code for the second terminal window which will represent node 2. 

```
(Terminal Window 2)
./geth --datadir node2 --unlock NODE2_PUBLIC_ADDRESS --mine --port 30304 --bootnodes enode://NODE1_ENODE_ADDRESS_THE_P2P_STUFF_YOU_COPIED --ipcdisable --allow-insecure-unlock
```
I hope I was able to clearly express where to put the data you have been saving from previous steps. But, now at this point, your private PoA blockchain should be running.

I will personally say that while this is a very simple step by step process many hiccups can occur and be very frustrating, it took me a couple of times to get everything running myself, so I am hoping to get everything conveyed as clearly as possible.

### Testing
Now that we have the actual blockchain running using our Go Ethereum Tools, we will test our work using MyCrypto. Hopefully you have already opened MyCrypto out of curiosity, but at this point we will be jumping into connecting our blockchain to MyCrypto. ***At this point I actually have some videos located in the screenshots folder. For these next few steps you would watch "connecting_node_to_mycrypto.mov"***

1. Click "Change Network" at the bottom left after opening MyCrypto.
![select change](/Screenshots/change_network_select.png)

2. Scroll all the way down, focusing on the right scroll window of the app and once at the bottom you will find "Add Custom Node". Click on "Add Custom Node".
![add custom node](/Screenshots/add_custom_node.png)

3. Here you will add the custom network information that you set in genesis, the first steps involving puppeth. The Node Name you can assign as the Network Name you initially created. Above I had Chrisbank in the example. The Network would be assigned to Custom. The Network Name would be the actual Network Name you created, I had Chrisbank as my example. Your currency will be ETH. The Chain ID will be the Chain ID I told you to make not of. I used 31313 in the example above. The URL will be the default URL so it will route to your local network:
http://127.0.0.1:8545. You will then select "Save & Use Custom Node" (***Again this can all be found in the video with another example setup and in the example picture below this is ANOTHER network I have created***)
![add custom info](/Screenshots/add_custom_network_info.png)


4. Now the network is connected and can be tested. We will now test it by sending money between accounts. ***This video can be found in the screenshots folder under "connecting_node_keystore_to_wallet.mov***. Back on the main page we will select "Keystore File" at the bottom middle in the "How would you like to access your wallet?" section.
![select how](/Screenshots/how_would_you_like_to_access.png)

5. The next screen will allow you to "Unlock your Keystore File". Here you will need the keystore file for your node1 and to remember the password you initially created for your node1. You well select "SELECT WALLET FILE" and then go to the keystore file which will be in your "Blockchain-Tools" folder,if you put it there like I suggested, under the folder representing your node1 under the "keystore" folder. The file will start with "UTC". You will select that file and then in the password section type in your node1 password.
![select wallet file](/Screenshots/select_wallet_file.png)

6. Your account wallet should now be opened inside of MyCrypto. You should now see the money we pre-funded the account in the genesis configuration. Feels good to be a millionaire right? This is only testing money, don't get crazy. At this point, we can go to the "to address" section, paste the public address for the second node we created, and send money. ***I have a video of all of this and how to check if it sent in the screenshots section under send_money_to_node_2.mov***
![send address example](/Screenshots/sending_money_address_ex.png)
![confirm transaction](/Screenshots/confirm_transaction.png)
After confirming the transaction you can then check the status to see how it went. A green banner will appear at the bottom of your wallet screen where you can click "Check TX Status" it will log you out, but you can follow the transaction to see if it was successful
![check status](/Screenshots/check_status.png)
Finally, if everything was successful you should see this.
![succesful transaction](/Screenshots/successful_transaction.png)
DONE!!


























