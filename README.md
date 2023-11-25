# YouTube Channels Analysis
This project involves using Pandas and Python to analyze and evaluate a dataset related to YouTube channels. The primary focus is on sorting and importing the dataset, computing the distribution of channel types, refining and importing data into a MySQL database, and executing queries to demonstrate interaction with the database.

## Getting Started

### Prerequisites

- Python environment
- Pandas library
- MySQL server

### Installing

1. **Python and Pandas:**
   ```bash
 pip install pandas
 
 ![image](https://github.com/Pavithra-thiru/Assignment-5/assets/151902813/2c4c39dd-3667-4104-9d6b-f7c2353efc73)
 
 To import the Pandas library into our Python environment, we use the command "import pandas".
 Using the abbreviation "pd" instead of "pandas" improves code readability.

 1. MySQL:
Install and set up a MySQL server.

2. Additional Libraries:
Ensure you have other necessary libraries installed as well.
**Running the Tests
Breakdown of Tests**
1. Sorting and Importing Dataset

    Purpose: Import the YouTube dataset for further analysis.
    Procedure:
        Use the Pandas library to read the dataset into a DataFrame.
        Address encoding problems if any.
![image](https://github.com/Pavithra-thiru/Assignment-5/assets/151902813/572882b9-9a29-4e28-a1cf-29eff65830b8)

•	The dataset is read into a Pandas DataFrame using the pd.read_csv() method.
•	The dataset's possible encoding problems are addressed using the argument encoding='latin-1'.

2. Sorting the Data Frame

![image](https://github.com/Pavithra-thiru/Assignment-5/assets/151902813/006c5bbb-51e9-47e2-a046-14ca65c118bf)

    Purpose: Sort the DataFrame in descending order based on the 'Subscribers' column.
    Procedure:
        Use the sort_values() function to arrange the DataFrame based on 'Subscribers.'
        
•	The DataFrame is arranged in descending order according to the 'Subscribers' column using the sort_values() function.
•	The sorting column is specified by the by argument, and a descending order is guaranteed by the ascending=False setting.

3. Calculating Channel Distribution

![image](https://github.com/Pavithra-thiru/Assignment-5/assets/151902813/1968d757-f485-4a8e-9dd0-856bc8bea517)

    Purpose: Analyze the distribution of channel types from the top 1000 records.
    Procedure:
        Use the calculate_channel_distribution function to determine the percentage of each unique channel type.

4. Loading Top 1000 Records
   
![image](https://github.com/Pavithra-thiru/Assignment-5/assets/151902813/70c4c4b7-b355-4385-a1fb-fd45dbf6c922)

    Purpose: Load only the top 1000 records into a separate CSV file and DataFrame.
    Procedure:
        Use the load_data_top_1000 function to create a new DataFrame with the top 1000 records.
        Save the refined dataset into a CSV file named 'top_1000_channels.csv.'

6. Deployment to MySQL

![image](https://github.com/Pavithra-thiru/Assignment-5/assets/151902813/da96eed2-d65e-4da0-b1db-f4ac36c86922)

    Purpose: Load the top 1000 records into a MySQL database.
    Procedure:
        Establish a connection with the MySQL server.
        Add 'top_1000_channels.csv' to the MySQL database.

Deployment

To deploy the project, follow the steps mentioned in the "Running the Tests" section.

**Author**

Pavithra Thirukumaran

**License**

This project is licensed under the [License Name] - see the LICENSE.md file for details.
**
Acknowledgement**

References

Altrad, O. (n.d.). Data 1202 - Data Analysis Tools Analytics. In Week 7 Class notes, presentations and Labs. 
Altrad, O. (n.d.). Data 1202 - Data Analysis Tools Analytics. In Week 8 Class notes, Presentations and Labs. 

Syntax
import pandas as pd

# Load the dataset
data1 = pd.read_csv('youtube_dataset.csv', encoding='latin-1')

# Sort the DataFrame by 'Subscribers' column in descending order
data= data1.sort_values(by='subscribers', ascending=False)

# Function to calculate the distribution of channeltype from the top 1000 records
def calculate_channel_distribution(data):
    channel_distribution = data['channeltype'].value_counts(normalize=True)
    return channel_distribution

def load_data_top_1000(data):
    top_1000_data = data.head(1000)
    top_1000_data.to_csv('top_1000_channels.csv', index=False)
    return top_1000_data

# Calculate channel distribution
channel_distribution_result = calculate_channel_distribution(data)
print(channel_distribution_result)

# Call the load_data_top_1000 function
top_1000_data = load_data_top_1000(data)

# Display the loaded DataFrame
top_1000_data.head()

# Display the loaded DataFrame
top_1000_data.head()

data2 = pd.read_csv('top_1000_channels.csv')
data2.head()

# Load library to connect Python and MySQL
pip install pymysql

# How to create an engine and connect to a database
# import required libraries
import pandas as pd
from sqlalchemy import create_engine
import pymysql

# create engine
engine = create_engine('mysql+pymysql://root:8699603125@localhost/assignment4')

# connection string
conn = engine.connect()

# read a simple query into DataFrame
df = pd.read_sql("SELECT * FROM assignment4.youtube_dataset", conn)

# print DataFrame
print(df.head())

# Specify the table name in the database
table_name = 'top_1000_channels.csv'

# Write the DataFrame to the MySQL table
data2.to_sql(table_name, con=engine, if_exists='replace', index=False)
