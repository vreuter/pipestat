<script>
document.addEventListener('DOMContentLoaded', (event) => {
  document.querySelectorAll('h3 code').forEach((block) => {
    hljs.highlightBlock(block);
  });
});
</script>

<style>
h3 .content { 
    padding-left: 22px;
    text-indent: -15px;
 }
h3 .hljs .content {
    padding-left: 20px;
    margin-left: 0px;
    text-indent: -15px;
    martin-bottom: 0px;
}
h4 .content, table .content, p .content, li .content { margin-left: 30px; }
h4 .content { 
    font-style: italic;
    font-size: 1em;
    margin-bottom: 0px;
}

</style>


# Package `pipestat` Documentation

## <a name="PipestatManager"></a> Class `PipestatManager`
pipestat standardizes reporting of pipeline results. It formalizes a way for pipeline developers and downstream tools developers to communicate -- results produced by a pipeline can easily and reliably become an input for downstream analyses. The ovject exposes API for interacting with the results can be backed by either a YAML-formatted file or a PostgreSQL database.


```python
def __init__(self, name, schema_path=None, results_file=None, database_config=None)
```

Initialize the object
#### Parameters:

- `name` (`str`):  namespace to report into. This will be the DB tablename if using DB as the object back-end
- `schema_path` (`str`):  path to the output schema that formalizesthe results structure
- `results_file` (`str`):  YAML file to report into, if file is used asthe object back-end
- `database_config` (`str`):  DB login credentials to report into,if DB is used as the object back-end




```python
def check_connection(self)
```

Check whether a PostgreSQL connection has been established
#### Returns:

- `bool`:  whether the connection has been established




```python
def check_record_exists(self, record_identifier)
```

Check if the record exists
#### Parameters:

- `record_identifier` (`str`):  unique identifier of the record


#### Returns:

- `bool`:  whether the record exists




```python
def check_result_exists(self, record_identifier, result_identifier)
```

Check if the result has been reported
#### Parameters:

- `record_identifier` (`str`):  unique identifier of the record
- `result_identifier` (`str`):  name of the result to check


#### Returns:

- `bool`:  whether the specified result has been reported for theindicated record in current namespace




```python
def close_postgres_connection(self)
```

Close connection and remove client bound



```python
def data(self)
```

Data object
#### Returns:

- `yacman.YacAttMap`:  the object that stores the reported data




```python
def db_cursor(self)
```

Establish connection and get a PostgreSQL database cursor, commit and close the connection afterwards
#### Returns:

- `LoggingCursor`:  Database cursor object




```python
def establish_postgres_connection(self, suppress=False)
```

Establish PostgreSQL connection using the config data
#### Parameters:

- `suppress` (`bool`):  whether to suppress any connection errors


#### Returns:

- `bool`:  whether the connection has been established successfully




```python
def file(self)
```

File path that the object is reporting the results into
#### Returns:

- `str`:  file path that the object is reporting the results into




```python
def name(self)
```

Namespace the object writes the results to
#### Returns:

- `str`:  Namespace the object writes the results to




```python
def remove(self, record_identifier, result_identifier=None)
```

Report a result.

If no result ID specified or last result is removed, the entire record
will be removed.
#### Parameters:

- `record_identifier` (`str`):  unique identifier of the record
- `result_identifier` (`str`):  name of the result to be removed or Noneif the record should be removed.


#### Returns:

- `bool`:  whether the result has been removed




```python
def report(self, record_identifier, result_identifier, value, force_overwrite=False, strict_type=True)
```

Report a result.
#### Parameters:

- `record_identifier` (`str`):  unique identifier of the record, value toin 'record_identifier' column to look for to determine if the record already exists
- `value` (`any`):  value to be reported
- `result_identifier` (`str`):  name of the result to be reported
- `force_overwrite` (`bool`):  whether to overwrite the existing record


#### Returns:

- `bool`:  whether the result has been reported




```python
def result_schemas(self)
```

Result schema mappings
#### Returns:

- `dict`:  schemas that formalize the structure of each resultin a canonical jsonschema way




```python
def retrieve(self, record_identifier, result_identifier=None)
```

Retrieve a result for a record.

If no result ID specified, results for the entire record will
be returned.
#### Parameters:

- `record_identifier` (`str`):  unique identifier of the record
- `result_identifier` (`str`):  name of the result to be retrieved


#### Returns:

- `any | dict[any]`:  a single result or a mapping with all theresults reported for the record




```python
def schema(self)
```

Schema mapping
#### Returns:

- `dict`:  schema that formalizes the results structure




```python
def validate_schema(self)
```

Check schema for any possible issues
#### Raises:

- `SchemaError`:  if any schema format issue is detected







*Version Information: `pipestat` v0.0.1, generated by `lucidoc` v0.4.3*