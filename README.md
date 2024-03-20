# Cosmos-SDK-EVMOS-Tutorial
Create your own blockchain and Validator Nodes using the Cosmos SDK and EVMOS - A simple to follow tutorial (Docker image and link to cosmos sdk official docs[https://tutorials.cosmos.network/tutorials/2-setup/])

## Its easy Getting Started
1. Install the lastest GO version[https://go.dev/doc/install] and remove previous versions

Linux CLI:
```
     rm -rf /usr/local/go
     cd /usr/local
     wget https://go.dev/dl/go1.22.1.linux-amd64.tar.gz
     tar -C /usr/local -xzf go1.22.1.linux-amd64.tar.gz
     run -> $ go version in CLI -> Expected result: go version go1.22.1 linux/amd64
```
2. 

3. Install node      ```sudo apt install npm```
4. install GNUmake   ```sudo apt install make```
5. install Rust      ```curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh```
6. Pull the cosmos SDK from github and clone it to /home/cosmos/cosmos-sdk
   Make sure you are using the same version as below v0.45.4
   ```
   mkdir cosmos
   cd cosmos
   git clone https://github.com/cosmos/cosmos-sdk
   cd cosmos-sdk
   git checkout v0.45.4 

   ```
8. If Everything was installed correctly, you should be able to run in /home/cosmos/cosmos-sdk/
   ```make build```
   once the build has been completed without errors.
   run ```./build/simd version``` which should return 0.45.4.

All the steps above are described in the [cosmos.network tutorials portal]([https://tutorials.cosmos.network/tutorials/3-run-node/#run-a-node-api-and-cli])

## How to Use the Cosmos SDK to Run a Node, API, and CLI
11. [watch this short vid to review the next steps](https://youtu.be/wNUjkp2PFQI)
