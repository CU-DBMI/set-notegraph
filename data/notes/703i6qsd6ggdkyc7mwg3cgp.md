
Tools for data validation.

## Schema-based Validation

Using static schema definitions to validate data.

### Apache-project Based

- [Avro (pythonic implementation)](https://avro.apache.org/docs/1.11.1/getting-started-python/): Python library for using [Apache Avro](https://avro.apache.org/docs/).
- [Apache Arrow Table Schema Validate (PyArrow)](https://arrow.apache.org/docs/python/generated/pyarrow.Table.html#pyarrow.Table.validate): Validates [Apache Arrow](https://arrow.apache.org/docs/index.html) schema.
- [Apache Parquet Schema (PyArrow)](https://arrow.apache.org/docs/python/generated/pyarrow.parquet.ParquetFile.html#pyarrow.parquet.ParquetFile.schema): Gathers but no embedded validate functionality for Parquet-based schema. Note: may use Arrow-based schema validation through PyArrow.

### JSON-based

- [jsonschema (pythonic implementation)](https://python-jsonschema.readthedocs.io/en/stable/): Python library for using [JSON Schema](https://json-schema.org/) functionality.

### Independent

- [Cerberus](https://github.com/pyeve/cerberus): custom data validation system for python.
- [Deequ](https://github.com/awslabs/deequ): schema and profile based data unit-testing framework based on [Apache Spark](https://spark.apache.org/).
- [Pydantic](https://pydantic-docs.helpmanual.io/): Pythonic data validation library.
- [Marshmallow](https://marshmallow.readthedocs.io/en/stable/): Pythonic data ORM/ODM and validation library.
- [Pandas `assert_frame_equal`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.testing.assert_frame_equal.html): validate Pandas dataframes against one another.
- [Pandera](https://pandera.readthedocs.io/en/latest/index.html): Pythonic dataframe-focused schema validation.
- [Voluptuous](https://github.com/alecthomas/voluptuous): custom data validation system for python.
- [Schema (Python)](https://github.com/keleshev/schema): Pythonic schema validation.

### Language

- [Cuelang](https://cuelang.org/): data, schema, and validation language, all-in-one.

## Profile-based Validation

Using profiles of data (as opposed to static schema definition) to validate data.

- [Great Expectations](https://docs.greatexpectations.io/docs/): implements profile-based data quality checks and validation for your data.
- [Soda](https://docs.soda.io/soda/quick-start-soda-core.html): implements profile-based data quality checks and validation for your data.
- [DeepChecks](https://docs.deepchecks.com/stable/getting-started/welcome.html): intended from ML data profile validation.
