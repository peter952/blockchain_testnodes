## Steps in Genesis block creation for testchain with two nodes

* Step 1:
Create accounts for two nodes for the network with a separate datadir for each using geth.

```
./geth --datadir node1 account new
./geth --datadir node2 account new


```

![](Screenshots/new_accounts.PNG)

Save newly created sealer addresses for when needed 

* Step 2:
Run puppeth, name your network, and select the option to configure a new genesis block.

Choose the Clique (Proof of Authority) consensus algorithm.

Paste both account addresses from the first step one at a time into the list of accounts to seal.

```
./puppeth
```
![](Screenshots/Puppeth_set_up.PNG)

Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

You can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.

![](Screenshots/set_up.PNG)

* Step 3
With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

Using geth, initialize each node with the new networkname.json.

```
./geth --datadir node1 init networkname.json
./geth --datadir node2 init networkname.json
```

![](Screenshots/node_int.PNG)

* Step 4:
Now the nodes can be used to begin mining blocks.

Run the nodes in separate terminal windows with the commands:

```
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
```
* Step 5:
Open the MyCrypto app, then click Change Network at the bottom left:
Click "Add Custom Node", then add the custom network information that you set in the genesis.

Make sure that you scroll down to choose Custom in the "Network" column to reveal more options like Chain ID:
Type ETH in the Currency box.

In the Chain ID box, type the chain id you generated during genesis creation.

In the URL box type: "Your HTTP here" This points to the default RPC port on your local machine.

Finally, click Save & Use Custom Node.

* Step 6:
After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.

Select the View & Send option from the left menu pane, then click Keystore file.
On the next screen, click Select Wallet File, then navigate to the keystore directory inside your Node1 directory, select the file located there, provide your password when prompted and then click Unlock.

This will open your account wallet inside MyCrypto.
In the To Address box, type the account address from Node2, then fill in an arbitrary amount of ETH:
Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.

![](Screenshots/confirmation.PNG)


