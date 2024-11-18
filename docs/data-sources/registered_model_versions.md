---
subcategory: "Unity Catalog"
---
# databricks_registered_model_versions Data Source

-> This resource can only be used with a workspace-level provider!

This resource allows you to get information about versions of [Model in Unity Catalog](https://docs.databricks.com/en/mlflow/models-in-uc.html).

## Example Usage

```hcl
data "databricks_registered_model_versions" "this" {
  full_name = "main.default.my_model"
}
```

## Argument Reference

The following arguments are supported:

* `full_name` - (Required) The fully-qualified name of the registered model (`catalog_name.schema_name.name`).

## Attribute Reference

The following attributes are exported:

* `model_versions` - list of objects describing the model versions. Each object consists of following attributes:
  * `aliases` - the list of aliases associated with this model. Each item is object consisting of following attributes:
    * `alias_name` - string with the name of alias
    * `version_num` - associated model version
  * `catalog_name` - The name of the catalog where the schema and the registered model reside.
  * `comment` - The comment attached to the registered model.
  * `created_at` - the Unix timestamp at the model's creation
  * `created_by` - the identifier of the user who created the model
  * `full_name` - The fully-qualified name of the registered model (`catalog_name.schema_name.name`).
  * `id` - The unique identifier of the model version
  * `metastore_id` - the unique identifier of the metastore
  * `model_version_dependencies` - block describing model version dependencies, for feature-store packaged models. Consists of following attributes:
    * `dependencies` - list of dependencies consisting of following attributes:
      * `function` - A function that is dependent on a SQL object:
        * `function_full_name` - Full name of the dependent function
      * `table` - A table that is dependent on a SQL object
        * `table_full_name` - Full name of the dependent table
  * `name` - The name of the registered model.
  * `owner` - Name of the registered model owner.
  * `run_id` - MLflow run ID used when creating the model version, if `source` was generated by an experiment run stored in an MLflow tracking server
  * `run_workspace_id` - ID of the Databricks workspace containing the MLflow run that generated this model version, if applicable
  * `schema_name` - The name of the schema where the registered model resides.
  * `source` - URI indicating the location of the source artifacts (files) for the model version.
  * `status` - Current status of the model version.
  * `storage_location` - The storage location under which model version data files are stored.
  * `updated_at` - the timestamp of the last time changes were made to the model
  * `updated_by` - the identifier of the user who updated the model last time
  * `version` - Integer model version number, used to reference the model version in API requests.

## Related Resources

The following resources are often used in the same context:

* [databricks_registered_model](registered_model.md) data source to retrieve information about a model within Unity Catalog.
* [databricks_registered_model](../resources/registered.md) resource to manage models within Unity Catalog.
* [databricks_model_serving](../resources/model_serving.md) to serve this model on a Databricks serving endpoint.
* [databricks_mlflow_experiment](../resources/mlflow_experiment.md) to manage [MLflow experiments](https://docs.databricks.com/data/data-sources/mlflow-experiment.html) in Databricks.