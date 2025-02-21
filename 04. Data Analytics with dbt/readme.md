
Install dbt cli way
using pip: https://docs.getdbt.com/docs/core/pip-install
- Go to a folder in your machine:
- make a venv
- activate the venv
- then install dbt-core and postgres plugin, if you want to use postgres: 
python -m pip install dbt-core dbt-postgres
- then make a new folder to create a starter project.
- 





dbt connects to and runs SQL against your database, warehouse, lake, or query engine. These SQL-speaking platforms are collectively referred to as **data platforms**. dbt connects with data platforms by using a dedicated **adapter plugin** for each. Plugins are built as Python modules that dbt Core discovers if they are installed on your system.
To install an adapter(eg. Redshift)

git clone https://github.com/dbt-labs/dbt-redshift.git
cd dbt-redshift
python -m pip install .




