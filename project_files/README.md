# Group 11 Term Project - Migraine Dataset

This project pulls posts from Migraine Subreddit, Migraine.com, and Patient.info and extracts information about peoples experiences that include following features:

- Age
- Gender
- Suicidal thoughts
- Presence of aura
- Migraine triggers
- ADHD
- Treatments/drugs and dosage
- Effectiveness of treatments

# Dataset

Migraine Dataset produced for this term is located in data\migraine_all_group11.csv

# Files

- reddit2db.ipynb - Retrieves Migraine Subreddit date from Pushshift.io server and stores in database.
- reddit_db_2db.ipynb - Converts Reddit Migraine Subreddit data in MongoDB into CSV file containing only the fields of interest.
- migraine_forum_data_extraction.ipynb - Scrapes Migraine.com website and stores posts into CSV file.
- patient_info_data_extraction.ipynb - Scrapes Patient.info website and stores posts int CSV file.
- feature_extraction.ipynb - Notebook documents every step we took to extract features and build final dataset.  This notebook is capable of building the final dataset from CSV files that contain gathered posts from our sources.
- easy_feature_extraction.ipynb - This notebook is similar to the above one but it contains only the functions needed to execute information extraction pipeline.  This notebook is here in case you want to build the dataset yourself quickly.  Approximate run time is ~30 minutes.
- group_11_proposal.ipynb - Original notebook submitted for project propose.  Included here for reference.
- DSCI511_term_project_group_11.ipynb - PDF of our PowerPoint presentation.
- *.excalidraw - Diagrams used in the presentation.
- docker-compose.yml - Docker compose for starting MongoDB database.

# Data

All data files are stored in `data` folder.

- migraine_all_group11.csv - Final migraine dataset.
- reddis_migraine_posts.csv - input data gathered from Migraine Subreddit in CSV format (using reddit2db.ipynb)
- migraine.com.csv - input data gathered from Migraine.com in CSV format (using migraine_forum_data_extraction.ipynb)
- patient.info.csv - input data gathered from patient.info in CSV format (using patient_info_data_extraction.ipynb)

# How to install dependencies

You can environment and install required dependencies with `poetry`:

- poetry shell
- poetry install

Or if you are using `pyenv` or some other Python environment and prefer pip based install:

- pip install -r requirements.txt

# What to run and how to run it

## Get posts from Reddit via Pushshift.io APIs and store them in CSV format

### MongoDB Setup

Rather than dealing with differences of MongoDB setup on different operating systems we decided to use Docker based approach.  Here is the `docker-compose.yml`:

```
version: "3"
services:
  mongo:
    image: mongo:latest
    volumes:
      - ./dbdata:/data/db
    ports:
      - 37017:27017

```

We start this using `docker-compose up -d`.  Notice we mapped `/data/db` which is default location for database files to host's `/dbdata`.  This allows restarts of the container without losing the data.  In addition, we can just zip `dbdata` folder to share database files.

You can verify that this is working by calling `mongo` client from host OS: `mongo localhost:37017`.

### Retrieve posts from Reddit into MongoDB

- Run reddit2db.ipynb - this will store all of the data in MongoDB

### Extract only needed fields and store posts as CSV file

- Run reddit_db_2_csv.ipynb - this will query posts data from MongoDB and create input data in `data/reddis_migraine_posts.csv`

## Get posts from Migraine.com and store them in CSV format

- Run migraine_forum_data_extraction.ipynb

## Get posts from patient.info and store them in CSV format

- Run patient_info_data_extraction.ipynb

## Extract the features and create final dataset

- Run easy_feature_extraction.ipynb


