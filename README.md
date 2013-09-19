s3cfg
=====

A small command line interface to work with configuration files on s3.

Make sure you have `boto` setup to connect to aws as shown [here](http://docs.pythonboto.org/en/latest/getting_started.html).

## Design

Store all config files in S3

Naming Scheme:

- `shared.json` Shared configuration details
- `my-project.json` Project-specific configuration details

Format:

```json
{
  "version": "1.0",
   ...
}
```

Proposed CLI:

```sh
s3cfg get my-project shared # Get latest shared.json and my-project.json
s3cfg get my-project.yaml@1.2 # Get version 1.2 of my-project only. output as yaml
s3cfg merge shared my-project # Gets both shared and my-project, merges and outputs as s3cfg.<date>.json

s3cfg put my-project.json # Ensure new version (in json). read my-project.json and push it. link latest
```

On deployment to a node.js project:

```
pushd config && s3cfg merge shared my-project --output production.json && popd
```