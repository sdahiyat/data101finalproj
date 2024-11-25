# Project Checkpoint
# Project Title: Analyzing User Reviews and Business Trends with PostgreSQL and MongoDB

Sierra Dahiyat, Sophia Ladyzhensky, Ananya Chawla, Aidana Jakulina

## Dataset Selection

The Yelp dataset comprises multiple JSON files, including yelp_academic_dataset_business.json, which provides detailed information about businesses with attributes such as business_id (primary key), name, address, city, review_count, and categories. Another important file, yelp_academic_dataset_review.json, contains user reviews for these businesses, including a primary key, review_id, and a foreign key, business_id, linking to the business dataset. Additionally, the dataset includes yelp_academic_dataset_user.json, which provides user-specific details with the primary key user_id. Finally, the dataset also features yelp_academic_dataset_checkin.json and yelp_academic_dataset_tip.json, both of which reference business_id and user_id as foreign keys.
Since the full Yelp academic dataset is approximately 10GB—exceeding the size limit for this project—we plan to reduce it to 1GB through sampling. This will involve selecting a random subset of 10,000 businesses and including only the related users and their reviews. In doing so, we will focus the data on a specific subset of businesses while preserving the relationships between users, businesses, and reviews. With an average of 100 reviews per business, this approach will yield approximately 1 million records, satisfying the requirements for dataset size and multiple foreign key relationships.
To sample the data, we will randomly select 10,000 businesses and filter the reviews and users to include only those associated with the selected businesses.

[ER Diagram]([url](https://dbdiagram.io/d/6743c567e9daa85aca8dd775))

## System and Database Setup

* Describe how you loaded data into Postgres, e.g. include code snippets, diagrams, etc.
* Are you using DataHub or your local computer(s) for compute resources? Are you using that same setup to store your database, or are you using another (cloud) system?

## PostgreSQL Tasks and Queries

* Overview of the problem(s) you are trying to solve

### Task / Query 1

(For each query)

* Describe the problem
* Explain why this is a reasonable solution
* Evaluate it's performance
* Show the query
* Show the output

## Future Plan (Checkpoint Only)

We plan to use MongoDB as our non-relational database system due to its ability to handle semi-structured data like JSON. MongoDB will allow us to store the dataset with minimal transformations, maintaining the natural structure of the data.

Examples of queries we would be covering: 
Top-Rated Businesses by City
Most Active Users
Top Categories by Review Volume
Business-Specific Reviews

We will compare PostgreSQL and MongoDB on:

1. Performance- Query execution times for filtering and aggregations.
2. Usability - Ease of writing and running queries.
3. Flexibility- Handling semi-structured data (MongoDB) vs. structured schema (PostgreSQL).
This comparison will help us determine which system is more suitable for specific use cases, such as analytical tasks or real-time querying.
