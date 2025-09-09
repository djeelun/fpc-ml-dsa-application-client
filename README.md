# 'FPC ML-DSA' Middleware Server
This middleware server relays requests from a client to be executed on the HLF blockchain.
This is part of my master's thesis project, which covers how to secure [HLF](https://hyperledger-fabric.readthedocs.io/en/release-2.5/) with [FPC](https://github.com/hyperledger/fabric-private-chaincode) against quantum adversaries. 
The full thesis can be found in the [TU Delft Repository](https://resolver.tudelft.nl/uuid:cec0b1bf-fc85-4d58-a4c0-6a81e184a3a7).

## Setup
This server is written in Go. To run this server:
  1. First, follow the installation/setup guide for the [FPC development container](https://github.com/hyperledger/fabric-private-chaincode/blob/main/docs/setup-option1.md).
  2. Launch a test deployment server by following [this guide](https://github.com/hyperledger/fabric-private-chaincode/blob/main/samples/deployment/test-network/README.md).
     This creates a test network with two organizations (1 peer each).
     The specific chaincode for our peers can be found at [djeelun/fpc-ml-dsa-contract](https://github.com/djeelun/fpc-ml-dsa-contract).
  4. When the network is up and running, we can start our middleware server. Clone the repo in a directory within ``$FPC_PATH``, say ``$FPC_PATH/samples/application``:
     ```bash
     cd $FPC_PATH/samples/application
     git clone https://github.com/djeelun/fpc-ml-dsa-application-client.git
     cd fpc-ml-dsa-application-client
     make init      # when running for the first time
     ```
  5. When running the server for the first time (after network setup), make sure to run ``make init``. This initializes the enclave. Otherwise, run ``make run``.

## Endpoints
The server exposes the following endpoints:
- ``/verifySig``, expects JSON ``{sig: string, m: string, ctx: string, pk: string, algo: integer}``.
- ``/putCipher``, expects JSON ``{cipherId: string, ciphertext: string}``.
- ``/getCipher``, expects JSON ``{cipherId: string}``.
- ``/updateCipher``, expects JSON ``{cipherId: string, token: string}``.

Our front-end can be found at [djeelun/fpc-ml-dsa-web-app](https://github.com/djeelun/fpc-ml-dsa-web-app).

## Contact
For any further questions you may have, feel free to contact me at [jaylan2993@gmail.com](jaylan2993@gmail.com).
