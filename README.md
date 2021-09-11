# Star Registry Private Blockchain Application

This application allows you to registar stars with owner informarion using private blockchain.

## To start this application
1. install Node.JS and download this repository
2. run "npm install" to install libraries
3. run "node app.js" to start web server
4. call endpoints to send HTTP requests to the web server

## Libraries
1. `bitcoinjs-lib` and `bitcoinjs-message`. Those libraries will help us to verify the wallet address ownership, we are going to use it to verify the signature.
2. `express` The REST Api created for the purpose of this project it is being created using Express.js framework.
3. `body-parser` this library will be used as middleware module for Express and will help us to read the json data submitted in a POST request.
4. `crypto-js` This module contain some of the most important cryotographic methods and will help us to create the block hash.
5. `hex2ascii` This library will help us to **decode** the data saved in the body of a Block.

## How to registar starts
To test the application, used POSTMAN to send HTTP requests and see response

1. create a Genesis Block by calling the endpoint http://localhost:8000/block/hight/0
   <img width="934" alt="スクリーンショット 2021-09-11 13 30 44" src="https://user-images.githubusercontent.com/20425552/132937093-bff7b69d-2fa9-4e53-aeeb-0481c876f919.png">

2. send a message to be signed using a Wallet and in this way verify the ownership over the wallet address.
   The message format will be: `<WALLET_ADRESS>:${new Date().getTime().toString().slice(0,-3)}:starRegistry`;
   <img width="934" alt="スクリーンショット 2021-09-11 13 31 01" src="https://user-images.githubusercontent.com/20425552/132937129-91ae1417-4b2f-4280-9704-4c3a28ec5005.png">
   
3. Once the user have the message, the user can use a Wallet to sign the message. Used Bitcoin Core for a sample. 
   <img width="730" alt="スクリーンショット 2021-09-11 13 32 09" src="https://user-images.githubusercontent.com/20425552/132937155-135cdae5-1bb3-41dc-beec-708f256c1fe2.png">

4. submit the Star object for that it will submit: `wallet address`, `message`, `signature` and the `star` object with the star information.
    The Start information will be formed in this format:
    ```json
        "star": {
            "dec": "68° 52' 56.9",
            "ra": "16h 29m 1.0s",
            "story": "Testing the story 4"
		}
    ```
    <img width="1007" alt="スクリーンショット 2021-09-11 13 31 27" src="https://user-images.githubusercontent.com/20425552/132937279-e88cf1f1-6656-44e5-89c6-b091498b0aca.png">    
    
5. The application will verify if the time elapsed from the request ownership (the time is contained in the message) and the time when you submit the star is less than 5 minutes.
6. If everything is okay the star information will be stored in the block and added to the `chain`
7. The application will allow us to retrieve the Star objects belong to an owner (wallet address). 
   <img width="1010" alt="スクリーンショット 2021-09-11 13 31 51" src="https://user-images.githubusercontent.com/20425552/132937298-2e97d52f-4077-4427-ae3f-cd81a21e3bb2.png">
