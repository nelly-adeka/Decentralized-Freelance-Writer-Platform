# Decentralized-Freelance-Writer-Platform
Créez une plateforme décentralisée pour les rédacteurs freelances, en utilisant des contrats intelligents pour garantir des paiements équitables et la protection des droits d'auteur.
from web3 import Web3
import json

# Connect to an Ethereum node
w3 = Web3(Web3.HTTPProvider('https://your_ethereum_node_url'))

# Load the compiled contract ABI
with open('FreelanceWriterPlatformABI.json', 'r') as file:
    contract_abi = json.load(file)

# Contract address after deploying FreelanceWriterPlatform.sol
contract_address = '0xYourContractAddress'

# Initialize contract
freelance_writer_platform = w3.eth.contract(address=contract_address, abi=contract_abi)

# Function to create a new writing gig
def create_gig(employer_address, deadline, payment):
    transaction = freelance_writer_platform.functions.createGig(deadline, payment).buildTransaction({
        'from': employer_address,
        'value': payment,
        'gas': 1000000,
        'nonce': w3.eth.getTransactionCount(employer_address),
    })
    # Sign and send the transaction
    # Note: This requires the private key which should be securely managed
    # signed_txn = w3.eth.account.signTransaction(transaction, private_key='YourPrivateKey')
    # tx_hash = w3.eth.sendRawTransaction(signed_txn.rawTransaction)
    # return tx_hash

# Example usage
# Assuming the employer wants to create a gig with a certain deadline and payment
# create_gig('0xEmployerWalletAddress', 1672531200, w3.toWei(0.1, 'ether'))

