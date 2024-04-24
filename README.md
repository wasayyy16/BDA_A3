# BDA_A3
PREPROCESSING: 
The code performing this is designed to preprocess a dataset stored in a JSON file. It begins by importing necessary libraries such as pandas for data manipulation and json for handling JSON files. The script then reads data from a specific JSON file location and parses each line into a Python dictionary, storing these dictionaries in a list.
Subsequently, the list of dictionaries is converted into a pandas DataFrame, facilitating easier data manipulation. Irrelevant columns are dropped from the DataFrame, and rows containing missing values are removed. The 'price' column undergoes cleaning, where dollar signs and hyphens are removed, and the values are converted into numeric format.
Finally, the preprocessed DataFrame is saved into a new JSON file named 'preprocessed_final1.json', ready for further analysis or use. Overall, the script streamlines data preparation tasks, ensuring the dataset is cleaned and structured appropriately for downstream analysis or modeling.
PRODUCER : 
This Python code is designed to facilitate the transfer of preprocessed data from a JSON file into a Kafka topic. It begins by importing necessary libraries, including json, time, and KafkaProducer from the kafka library. The KafkaProducer instance is initialized with the specified bootstrap server.
Next, key variables are defined, including the Kafka topic name ('assignment-topic') and the chunk size, which determines the number of records to be read from the JSON file at each iteration.
The script then enters a loop to read data from the JSON file in chunks. Within this loop, data is read and parsed into a list of dictionaries representing individual records. Each dictionary is converted into a JSON string, encoded into bytes using UTF-8, and sent to the Kafka topic using the send() method of the KafkaProducer instance. A brief pause of 1 second is introduced between each message to control the rate of data publishing. Additionally, a message indicating that the data has been published is printed for each record.
After publishing all data from the file, the producer is flushed to ensure all pending messages are sent, and then it's closed to release resources.
In essence, this script provides a streamlined mechanism for transferring preprocessed data from a JSON file to a Kafka topic, enabling seamless integration into Kafka-based data pipelines or systems.
CONSUMERS : 
This Python code sets up a KafkaConsumer to receive messages from a Kafka topic named 'assignment-topic'. It's designed to perform real-time analysis on these messages using the Apriori algorithm, which extracts frequent itemsets and generates association rules.
Initially, the script defines parameters such as the minimum support and confidence thresholds to filter out less significant itemsets and rules. It then initializes data structures to store frequent itemsets and counts, along with a counter for total transactions processed.
The core of the script lies in the generation of frequent itemsets and association rules. For each incoming message, the script decodes and parses it, treating it as a transaction. It incrementally updates the counts of itemsets based on the transaction data and prunes infrequent itemsets according to the minimum support threshold.
As the script iterates over the messages, it generates association rules from the frequent itemsets meeting the minimum confidence threshold. Real-time insights, including the current frequent itemsets and generated association rules, are printed after processing each transaction.
Once all messages have been processed, the KafkaConsumer instance is closed, completing the real-time analysis pipeline. This script enables continuous monitoring and analysis of incoming data streams, providing valuable insights into patterns and associations within the data.

This code establishes a KafkaConsumer to receive messages from the Kafka topic named 'assignment-topic'. Its purpose is to perform real-time analysis using the PCY algorithm, aiming to identify frequent itemsets and generate association rules from the incoming transactions.
The script begins by initializing data structures, including dictionaries for counting single items (itemsets) and item pairs (item_pairs). Additionally, an empty list (association_rules) is created to store the generated association rules.
PCY algorithm parameters such as the hash bucket size (hash_bucket_size) and a bitmap (bitmap) to track hash collisions are defined to facilitate the algorithm's execution.
As messages are received from the Kafka topic, they are processed iteratively. Each message is decoded from bytes to a string and parsed as JSON to represent a transaction.
Subsequently, the script updates the itemsets dictionary with the counts of single items and calculates the counts of item pairs in each transaction. It also updates the bitmap based on hash collisions.
For each frequent item pair, the script calculates the confidence of the association rule and adds it to the association_rules list if it exceeds the threshold of 0.5.
Real-time insights, including the current frequent itemsets and generated association rules, are printed after processing each transaction to provide ongoing visibility into the analysis process.
Upon processing all messages, the KafkaConsumer instance is closed, marking the completion of the real-time analysis pipeline. Overall, this script enables continuous monitoring and analysis of transaction data streams, offering valuable insights into patterns and associations within the data.


This Python script sets up a KafkaConsumer to receive messages from the Kafka topic named 'assignment-topic'. It implements the ELCAT (Essential Learning for Classification Association Trees) algorithm, aiming to identify frequent itemsets in real-time.
The script initializes parameters such as the minimum support threshold (min_support) to determine the significance of itemsets. Additionally, it sets up data structures including a defaultdict (itemset_support) to store support counts for itemsets and a counter (total_transactions) to track the total number of processed transactions.
Two functions are defined within the script:
update_support(transaction): This function updates the support counts of itemsets based on each transaction received.
prune_itemsets(): This function prunes infrequent itemsets from the itemset_support dictionary based on the defined minimum support threshold.
As messages are received from the Kafka topic, they are decoded and parsed as JSON to represent transactions. For each transaction, the script updates the support counts of itemsets and prunes infrequent itemsets accordingly. Real-time insights, including the current frequent itemsets along with their support counts, are printed after processing each transaction.
Once all messages have been processed, the KafkaConsumer instance is closed, completing the real-time analysis process. In summary, this script enables continuous monitoring and identification of frequent itemsets from streaming data, providing valuable insights into itemset support counts as data flows through the Kafka topic.

All the consumers are linked with some database at the end to store the data.


CONCLUSION: 
The preprocessing script cleans and structures a dataset stored in a JSON file, preparing it for further analysis. The producer script facilitates the transfer of preprocessed data to a Kafka topic, ensuring seamless integration into data pipelines. The consumer scripts then leverage various algorithms (Apriori, PCY, ELCAT) to perform real-time analysis on the data streamed from the Kafka topic, identifying frequent itemsets and generating association rules.
Each consumer script iterates over incoming messages, decoding and parsing them as transactions, and updates the necessary data structures accordingly. Real-time insights, including frequent itemsets and association rules, are printed during processing. Finally, all consumers are linked with a database to store the analyzed data.
In summary, these scripts form an end-to-end data pipeline, enabling continuous monitoring, analysis, and storage of streaming data from the Kafka topic, providing valuable insights into data patterns and associations.

