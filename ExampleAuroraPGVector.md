# pgvector Extension Queries

Welcome to the pgvector extension queries repository! This repository provides a collection of queries and examples to help you get started with the pgvector extension for PostgreSQL. The pgvector extension allows for efficient storage and querying of vector data, enabling advanced analytics and similarity searches.

## Installation

To get started with the pgvector extension, follow these steps:

1. Clone the pgvector repository from GitHub: [https://github.com/ankane/pgvector](https://github.com/ankane/pgvector)
2. Navigate to the cloned repository.
3. Follow the installation instructions provided in the repository's README file to build and install the extension.

## Queries

Explore the power of pgvector with these example queries

1. **Create the `vector` extension:**
  ` CREATE EXTENSION vector;`



2. **Create a table with a vector column:**

CREATE TABLE my_table (
  id SERIAL PRIMARY KEY,
  vector_col VECTOR
);

3. **Insert a row with a vector value into my_table:**

`INSERT INTO my_table (vector_col)
VALUES ('{1.2, 3.4, 5.6}');
`

# pgvector Extension Queries

Welcome to the pgvector extension queries repository! This repository provides a collection of queries and examples to help you get started with the pgvector extension for PostgreSQL. The pgvector extension allows for efficient storage and querying of vector data, enabling advanced analytics and similarity searches.

## Installation

To get started with the pgvector extension, follow these steps:

1. Clone the pgvector repository from GitHub: [https://github.com/ankane/pgvector](https://github.com/ankane/pgvector)
2. Navigate to the cloned repository.
3. Follow the installation instructions provided in the repository's README file to build and install the extension.

## Queries

Explore the power of pgvector with these example queries:
```sql

-- Create the `vector` extension
CREATE EXTENSION vector;

-- Create a table with a vector column
CREATE TABLE my_table (
  id SERIAL PRIMARY KEY,
  vector_col VECTOR
);

-- Insert a row with a vector value into `my_table`
INSERT INTO my_table (vector_col)
VALUES ('{1.2, 3.4, 5.6}');

-- Insert multiple rows with vector values into the `customer` table
INSERT INTO customer (name, vector_col)
VALUES
  ('John Smith', '[1.2, 3.4, 5.6]'),
  ('Jane Doe', '[0.8, 2.1, 4.5]'),
  ('Michael Johnson', '[2.3, 4.5, 6.7]'),
  ('Emily Davis', '[1.0, 2.0, 3.0]'),
  ('Robert Wilson', '[3.5, 1.2, 0.9]'),
  ('Olivia Thompson', '[2.1, 5.3, 1.8]'),
  ('William Lee', '[4.0, 2.5, 1.3]'),
  ('Sophia Brown', '[0.5, 3.2, 2.7]'),
  ('James Garcia', '[3.2, 1.9, 5.6]'),
  ('Ava Martinez', '[2.8, 4.1, 0.7]');

-- Perform a similarity search based on L2 distance in the `customer` table
SELECT id, name
FROM customer
ORDER BY vector_col <-> '[1.0, 2.0, 3.0]'
LIMIT 5;

-- Perform a similarity search based on cosine distance in the `customer` table
SELECT id, name
FROM customer
WHERE cosine_distance(vector_col, '[0.8, 2.1, 4.5]') > 0.9;

-- Perform a similarity search based on cosine distance in the `customer` table (with a different threshold)
SELECT id, name
FROM customer
WHERE cosine_distance(vector_col, '[0.8, 2.1, 4.5]') < 0.1;

-- Perform a similarity search based on cosine distance in the `customer` table (ordered by distance)
SELECT id, name
FROM customer
ORDER BY cosine_distance(vector_col, '[3, 1, 2]') ASC
LIMIT 5;

-- Upsert a row into the `customer` table
INSERT INTO customer (id, name, vector_col)
VALUES (1, 'John Smith', '[1.2, 3.4, 5.6]')
ON CONFLICT (id)
DO UPDATE SET name = EXCLUDED.name, vector_col = EXCLUDED.vector_col;

-- Update a row in the `customer` table
UPDATE customer
SET name = 'Jane Doe', vector_col = '[0.9, 2.3, 4.1]'
WHERE id = 1;

-- Delete a row from the `customer` table
DELETE FROM customer
WHERE id = 1;

-- Get the nearest neighbors to a specific vector in the `customer` table
SELECT *
FROM customer
WHERE id != 1
ORDER BY vector_col <-> (SELECT vector_col FROM customer WHERE id = 1)
LIMIT 5;

-- Calculate the average of vector values in the `customer` table
SELECT AVG(vector_col) FROM customer;

-- Calculate the average of vector values grouped by name in the `customer` table
SELECT name, AVG(vector_col) FROM customer GROUP BY name;

```
# Feel free to explore each query and adapt them to your specific use case.

# Contributions
## Contributions are welcome! If you have additional queries or examples that you would like to share, please submit a pull request. Let's build a comprehensive resource for the pgvector community!

# Resources
Here are some additional resources to help you further explore pgvector:

### pgvector Documentation: [Link to documentation]
### pgvector GitHub Repository: https://github.com/ankane/pgvector
### PostgreSQL Official Website: https://www.postgresql.org/
### Start leveraging the power of pgvector today and unlock new possibilities for your vector data storage and analysis!

# Happy querying!
