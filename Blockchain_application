#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Sep 16 13:04:57 2020

@author: mdtamjidhossain
"""

#%%
# importing library
import hashlib as hasher
import datetime as date
import random
from random import randint
import hashlib
import pickle
import random
#%%
number_of_blocks_to_add = 5


def create_genesis_block(genesis_block_header):
    genesis_block = dict()
    hashed_block = pickle.dumps(genesis_block_header)
    m = hashlib.sha256(hashed_block)
    current_hash = int(m.hexdigest(), 16)
    genesis_block = genesis_block_header
    genesis_block.update({'hash': current_hash})
    return genesis_block
#%%
# genesis transaction
print("---------------------Genesis Block----------------------" + "\n")
genesis_transaction ={
             'from': 'Genesis Block',
             'to': 'Genesis Block',
             'amount': 0
             }
print("Genesis Transaction: " + str(genesis_transaction) + "\n")
hashed_genesis_transaction = pickle.dumps(genesis_transaction)
genesis_transaction_hash = hashlib.sha256(hashed_genesis_transaction).hexdigest()

print("Genesis Root Hash: " + str(genesis_transaction_hash) + "\n")
#%%
genesis_block_header = {
    'index': 0,
    'timestamp': date.datetime.now(),
    'previousBlockHash': '0',
    'nonce': 0,
    'tx_root_hash': genesis_transaction_hash
}

print("Genesis Block: " + str(genesis_transaction_hash) + "\n")
print("--------------------------------------------------------" + "\n\n")
print("-------------------------New Block----------------------" + "\n")

# Create the blockchain and add the genesis block
# Genesis Mining to the blockchain
blockchain = [create_genesis_block(genesis_block_header)]

#%%
# Looping to add predefined number of blocks

for count in range(0,number_of_blocks_to_add):
    print(".........................Block Number: " + str(count+1) + "......................."+ "\n")    
    # Finding the last block 
    def last_block(blockchain):
        return blockchain[-1]
    
    #%%
    
    # randomly adding new transactions
    random_iteration = randint(2,6)                                 # there will be at least 2 transactions or 
                                                                    # at most 6 transactions per block
    transaction = dict()
    new_transaction_raw = []
    
    # keeping number of transaction even as merkle tree transaction structure follows binary structure which 
    # requires even number of transactions  
    if random_iteration % 2 == 0:
        random_iteration = random_iteration + 1
    
    for p in range(1,random_iteration):
        transaction_from = ['Anthony', 'Bill', 'Charles']           # selected three (03) persons as transaction sender
        transaction_to = ['Mark', 'Cooper', 'Damien']               # selected three (03) persons as transaction receiver
        random_transaction_from = random.choice(transaction_from)   # randomly selecting transaction sender
        random_transaction_to = random.choice(transaction_to)       # randomly selecting transaction receiver
        random_transaction_amount = randint(10, 30)                 # randomly selecting transaction amount within 
                                                                    # 10 usd to 30 usd. these amount can be changed.
        transaction ={
             'from': random_transaction_from,
             'to': random_transaction_to,
             'amount': random_transaction_amount
             }
            
        new_transaction_raw.append(transaction)                     # raw transaction list
        transaction = dict()
        
    print("New Transaction List: \n" + str(new_transaction_raw) + '\n')# raw transaction list
    
    # Hashing the new transactions
    new_transaction_hash_list = []
    for tran in new_transaction_raw:
        hashed_new_transactions = pickle.dumps(tran)
        new_transactions_hash = hashlib.sha256(hashed_new_transactions).hexdigest()
        
        new_transaction_hash_list.append(new_transactions_hash)
        new_transactions_hash = ''
    
    print("Hash of New Transaction List: \n" + str(new_transaction_hash_list) + "\n")
    #%%
    
    # Creating Merkle root of Transaction
    merkle_root_hash = new_transaction_hash_list
    
    i = 0
    j = 0
    while (len(merkle_root_hash)> 1):
        i = 0
        j = 0
        while i < len(merkle_root_hash):
            merkle_root_hash[j] = hashlib.sha256(str(merkle_root_hash[i] + 
                                                     merkle_root_hash[i+1]).encode('utf-8')).hexdigest()
            i = i + 2
            j = j + 1
            
        lastDelete = i - j
        del merkle_root_hash[-lastDelete:]
        if ((len(merkle_root_hash)>2) & (len(merkle_root_hash) % 2 != 0)):
            merkle_root_hash.append(merkle_root_hash[-1:][0])
        
        # print("Merkle hash tree: " + str(merkle_root_hash) + '\n') 
    print("New Transaction Root Hash: \n" + str(merkle_root_hash) + "\n")     
    #%%
    # new block
    block_header = {
        'index': last_block(blockchain)['index'] + 1,
        'timestamp': date.datetime.now(),
        'previousBlockHash': last_block(blockchain)['hash'],
        'nonce': 0,
        'tx_root_hash': merkle_root_hash[0]
    }
    print("New Transaction Block: \n" + str(block_header) + "\n")
    
    merkle_root_hash = []
    new_transaction_hash_list = []
    new_transaction_raw =[]
#%%    
    # Proof-of-work algorithm
    def proof_of_work(block_header):
        hashed_block = pickle.dumps(block_header)
        m = hashlib.sha256(hashed_block)
        
        # Set difficulty, the difficulty_hash below is the equivalent of requiring 2 zeros at the front of the hash
        difficulty_hash = 0x00FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
        # difficult_decimal = 1766847064778384329583297500742918515827483896875618958121606201292619775        
        # Set Miners involved and their respective CPU's
        alice = 3 * ['Alice'] # Represents 3 cpu units for alice
        bob = 5 * ['Bob'] # Represents 5 cpu units for bob
        charlie = 10 * ['Charlie'] # Represents 10 cpu units for charlie
        deborah = 1 * ['Deborah'] # Represents 1 cpu unit for deborah
        
        # Add Miners to an array and shuffle
        cpus = [alice, bob, charlie, deborah]
        miners = []
        for cpu in cpus:
            miners.extend(cpu)
        
        random.shuffle(miners)
        
        
        # While the hash is bigger than or equal to the difficulty continue to iterate the nonce
        while int(m.hexdigest(), 16) >= difficulty_hash:
            block_header['nonce'] += 1 # Increment nonce (ie change your guess)
            m = hashlib.sha256(pickle.dumps(block_header)) # Convert data to byte form so it can be hashed
            # print('Nonce Guess: ' + str(block_header['nonce']))
            # print('Resultant Hash: ' + str(m.hexdigest()))
            # print('Decimal value of hash: ' + str(int(m.hexdigest(), 16)) + '\n')
            miner = miners[block_header['nonce'] % len(miners)] # The miner who mined the block
            block_hash = m.hexdigest() # The hash of the blockheader with that nonce yields the block hash for 
                                       # that block
        
        # print(miners)
        # print('Valid Hash: ' + str(int(m.hexdigest(), 16)) + ' is less than ' + str(difficulty_hash))
        print('Miner who Mined Block: ' + miner + "\n\n")
        print("..................................................." + "\n" )
        
        resultant_hash = str(m.hexdigest())
        valid_hash = str(int(m.hexdigest(), 16))
        main_miner = miner
        nonce = str(block_header['nonce'])
        
        return resultant_hash, valid_hash, nonce, main_miner
 #%%   
    # getting the result of proof-of-work algorithm    
    # resultant_hash, valid_hash, guessed_nonce = proof_of_work(block_header)
    
    def is_valid_proof(block_header, resultant_hash, difficulty):
        return (resultant_hash.startswith('0' * difficulty))
    
    def add_block(block_header, resultant_hash, valid_hash, guessed_nonce, difficulty):
        previous_hash = last_block(blockchain)['hash']                                  # Call last_block function 
        if previous_hash != block_header['previousBlockHash']:
            return False
        if not is_valid_proof(block_header, resultant_hash, difficulty):                # Call is_valid_proof function 
            return False
            
        block_header.update({'hash': int(valid_hash)})
        block_header.update({'nonce': int(guessed_nonce)})
        blockchain.append(block_header)
        return True
    
    
    # New block Mining to the blockchain
    def mine_block(block_header, difficulty):
        resultant_hash, valid_hash, guessed_nonce, main_miner = proof_of_work(block_header)         # Call proof_of_work function 
        add_block(block_header, resultant_hash, valid_hash, guessed_nonce, difficulty)  # Call add_block function 
    
    difficulty = 4                                                                      # setting difficulty
    mine_block(block_header, difficulty)                                                # Call mine_block function
    count = count + 1                                                                   # increamenting the count of 
                                                                                        # block
print("--------------------------------------------------------" + "\n\n\n\n")
print("-------------------------Final Blockchain---------------" + "\n")
print(str(blockchain))    

#%%

