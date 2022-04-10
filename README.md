# Blockchain_project
Repository of the blockchain project, semester 2 PGDCLOUD NCI

# Docker Image
There is a Docker image available for testing on Dockerhub.
```
https://hub.docker.com/repository/docker/matyasgreff/tokendistribution
```
The application has been dockerized with preset values and distributes MTK tokens between 2 accounts.
To pull the image and run it, first make sure that docker is installed and the docker service is running, then pull and run the image.

### On Linux ###
```
docker --version
sudo service docker start
sudo docker pull matyasgreff/tokendistribution
sudo docker run matyasgreff/tokendistribution
```

### On Windows ###
First start Docker desktop, then:
```
docker pull matyasgreff/tokendistribution
docker run matyasgreff/tokendistribution
```

# Interaction with the code
Before doing anything, make sure to create a .env file in the root folder, set up these variables, and assign values to them:
```
INFURA_TOKEN=
CONTRACT_ADDRESS=
OWNER_ADDRESS=
SUPER_SECRET_PRIVATE_KEY=
```
Where INFURA_TOKEN is an infura.io issued token, CONTRACT_ADDRESS is the contract address of your token, OWNER_ADDRESS is the Metamask account ID(your own) on the ropsten or other test network. And SUPER_SECRET_PRIVATE_KEY is your secret key.
### Starting from zero ###
Create Infura and Metamask accounts, then simply copy and paste contracts/openzep_erc20.sol into Remix IDE, change name and symbol on line 180 and 181 to your liking, compile, then deploy in the Injected Web3 environment. Now check etherscan and validate the contract, then update CONTRACT_ADDRESS with the contract address of this token, also update other variables in .env.
### Run token distribution ###
The simplest way is to run it in a docker container.
Make sure to update accounts.txt with a list of accounts where you are looking to distribute tokens. They must be comma separated.
Then simply type :

```$docker-compose up```

To distribute to/from different accounts, modify the files accordingly then remove the existing image with: 

```$docker system prune -a -f```

Then run compose again:

```$docker-compose up```

It is necessary to rebuild the image each time you modify any of the files/variables, so the changes are in the image.

# Other features

Make sure node is installed on your host machine, then:
To install dependencies:
```$npm install```
To create a deterministic wallet:
```$node crypto/wallet.js```
To get information on contract, transfer to an account:(change variables, uncomment lines as needed in contract.js)
```$node contract.js```

