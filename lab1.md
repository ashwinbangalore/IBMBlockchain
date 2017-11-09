1. http://hyperledger-fabric.readthedocs.io/en/release/write_first_app.html
1. git clone https://github.com/hyperledger/fabric-samples.git
1. cd fabric-samples/fabcar
1. See what's inside the directory: enrollAdmin.js invoke.js package.json query.js registerUser.js  startFabric.sh
1. docker rm -f $(docker ps -aq)
1. Start the fabric: ./startFabric.sh
1. Install the SDK Node modules: npm install
1. node enrollAdmin.js
1. node registerUser.js
1. node query.js
