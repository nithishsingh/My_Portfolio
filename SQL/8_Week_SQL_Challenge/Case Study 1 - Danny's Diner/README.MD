# Interactive SQL Session

This repository provides options to conduct an interactive SQL session using various platforms and tools such as DB Fiddle, Jupyter Notebook, VS Code, Snowflake, Databricks, and BigQuery. You can choose the platform that best suits your preferences and familiarity.

## Platforms and Tools

### 1. Online Platforms:

- **DB Fiddle:** Access an interactive session within minutes by utilizing the DB Fiddle platform.

### 2. Local Development Environments:

- **Jupyter Notebook:** Utilize Jupyter Notebook for an interactive SQL session. 
  - Tools/libraries used: 
    - `ipython-sql` or `jupysql` for Jupyter integration with SQL
    - `psycopg2` for PostgreSQL database interaction
    - `sqlalchemy` for SQL toolkit and ORM

### Usage

Choose the platform or tool that suits your workflow:

#### DB Fiddle

1. Visit [DB Fiddle](https://www.db-fiddle.com/) and start an interactive session to write and execute SQL queries.

#### Jupyter Notebook

1. Install the required libraries:
   ```bash
   pip install ipython-sql jupyter psycopg2 sqlalchemy
   ```
2. Open Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
3. Create a new notebook and start writing SQL queries using the installed libraries (`ipython-sql`, `psycopg2`, `sqlalchemy`).

### Notes

- For users familiar with VS Code or Snowflake, Databricks, or BigQuery, feel free to utilize those platforms according to your preferences and expertise.
- Ensure you have the necessary permissions and credentials to access the databases on the chosen platforms.
- Modify the installation steps and tools based on your specific requirements.
