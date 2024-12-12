# NoSQL Challenge: UK Food Standards Analysis  

## Background  

The UK Food Standards Agency evaluates various establishments and assigns them a hygiene rating. This project involves analyzing this dataset for **Eat Safe, Love**, a food magazine that aims to identify notable establishments and trends for future articles.  

The challenge consists of three parts:  

1. **Database and Jupyter Notebook Setup**  
2. **Database Modifications**  
3. **Exploratory Analysis**  

This project uses MongoDB for storing and querying the data, and Python (with PyMongo and Pandas) for analysis.  

---

## Repository Structure  

The repository is organized as follows:  

```  
nosql-challenge/  
│  
├── Resources/  
│   └── establishments.json       # Initial dataset for MongoDB  
│  
├── NoSQL_setup_starter.ipynb     # Notebook for database setup and modifications  
├── NoSQL_analysis_starter.ipynb  # Notebook for exploratory analysis  
├── README.md                     # Project documentation  
├── requirements.txt              # Python dependencies  
├── .gitignore                    # Excluded files from version control  
│  
└── screenshots/                  # Screenshots of queries, plots, or results (optional)  
    ├── london_ratings.png        # Example: Results for London ratings query  
    ├── hygiene_scores.png        # Example: Hygiene scores by Local Authority  
```  

---

## Objectives  

### Part 1: Database and Jupyter Notebook Setup  

1. **Import Data**  
   - Import the `establishments.json` file into MongoDB using the following command in the terminal:  
     ```bash  
     mongoimport --db uk_food --collection establishments --file Resources/establishments.json --jsonArray  
     ```  
   - Confirm that the data has been successfully imported by listing the databases and collections in MongoDB.  

2. **Connect to MongoDB**  
   - Use PyMongo to connect to the MongoDB instance in `NoSQL_setup_starter.ipynb`.  
   - Verify the connection by retrieving and printing one document from the `establishments` collection.  

---

### Part 2: Database Modifications  

1. **Add a New Establishment**  
   - Add the following establishment to the database:  
     ```json  
     {  
       "BusinessName": "Penang Flavours",  
       "BusinessType": "Restaurant/Cafe/Canteen",  
       "BusinessTypeID": "",  
       "AddressLine1": "Penang Flavours",  
       "AddressLine2": "146A Plumstead Rd",  
       "AddressLine3": "London",  
       "PostCode": "SE18 7DY",  
       "LocalAuthorityName": "Greenwich",  
       "geocode": {  
         "longitude": "0.08384000",  
         "latitude": "51.49014200"  
       },  
       "Distance": 4623.9723280747176,  
       "NewRatingPending": true  
     }  
     ```  
   - Retrieve and update the `BusinessTypeID` for this new establishment.  

2. **Remove Unnecessary Data**  
   - Delete all documents with `LocalAuthorityName` as **Dover**.  

3. **Data Cleanup**  
   - Convert string-based numeric fields (`latitude`, `longitude`, and `RatingValue`) to appropriate numeric types using `update_many`.  

---

### Part 3: Exploratory Analysis  

1. **Hygiene Score Analysis**  
   - Identify establishments with a hygiene score of **20**.  

2. **Ratings in London**  
   - Find establishments in London with a `RatingValue` greater than or equal to **4**.  
   - Use a `$regex` query to match London-related `LocalAuthorityName`.  

3. **Top 5 Establishments Near Penang Flavours**  
   - Retrieve the top 5 establishments with a `RatingValue` of **5**, sorted by the lowest hygiene score and closest proximity to "Penang Flavours".  
   - Use geocode proximity with a ±0.01-degree range for latitude and longitude.  

4. **Hygiene Score of 0 by Local Authority**  
   - Count how many establishments have a hygiene score of **0** for each `LocalAuthorityName`.  
   - Sort results in descending order and display the top 10.  

---

## Installation  

1. **Clone the Repository**  
   ```bash  
   git clone https://github.com/your-username/nosql-challenge.git  
   cd nosql-challenge  
   ```  

2. **Install Python Dependencies**  
   ```bash  
   pip install -r requirements.txt  
   ```  

3. **Start MongoDB**  
   Ensure MongoDB is running locally or remotely before executing the notebooks.  

---

## Usage  

1. Open and execute `NoSQL_setup_starter.ipynb` to set up the database and apply modifications.  
2. Open and execute `NoSQL_analysis_starter.ipynb` to perform exploratory analysis.  

---

## Results  

### Example Outputs  

#### 1. Top 5 Establishments Near Penang Flavours  
| BusinessName     | Hygiene | RatingValue | Distance |  
|------------------|---------|-------------|----------|  
| Establishment A  | 0       | 5           | 0.002    |  
| Establishment B  | 1       | 5           | 0.003    |  

#### 2. Hygiene Scores of 0 by Local Authority  
| Local Authority   | Count |  
|-------------------|-------|  
| Thanet            | 1130  |  
| Greenwich         | 882   |  
