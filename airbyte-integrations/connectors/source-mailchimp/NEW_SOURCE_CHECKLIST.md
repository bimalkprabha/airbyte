# New python source checklist

This is an autogenerated file describing the high-level steps you need to take to implement a new Airbyte source in Python.

1. First, build the module by running the following from the `airbyte` project root directory:
   ```
   ./gradlew :airbyte-integrations:connectors:source-{dashCase name}:build
   ```
1. Define the specification for this source connector by modifying `source_mailchimp/spec.json`.
   A specification is a JSON file which uses JSONSchema to declare all the inputs needed for your integration to function 
   correctly. For example, if you were configuring a Postgres source, your specification might declare that you need a 
   `username` field which a string, a `password` field which is a string, a `host_url` which is a URI-formatted string, 
   and a `port` which is a `number`. The Airbyte UI will generate configurations that match the specification (by asking 
   the user to input them) and pass those configs to your source connector as input when it is being run.
   You can also manually generate config files and pass them to the integration CLI.
1. Implement your integration by editing `source_mailchimp/source.py` (and creating additional files as necessary).
    1. Implement the `Source` interface. For more information see the docstrings in `Source` and any parent classes.
    1. All logging should be done through the `logger` object passed into each method. Otherwise, logs will not be shown
       in the Airbyte UI.
1. Update the `sample_files` directory with an example config and catalog (discover output).
1. Create tests for your integration. 
    1. Unit tests go in the `unit_tests` folder. 
    1. Integration tests go in the `integration_tests` folder. Any tests that require external APIs or resources, you may need to give instructions on how to set up a testing instance/account for Airbyte's CI.
       However, for initial local development, you can place any sensitive credentials inside the `secrets/credentials.json` file -- this is gitignored by default. 
1. Update `README.md` to document the usage of your integration. If API credentials are required to run the integration, please document how they can be obtained or link to a how-to guide.
    1. For Airbyte core contributors, make sure to add the secret to RPass under the secret name as listed in `README.md`.
1. Add your source to the source definition registry in `airbyte-config/init`.

Once you've done all the above, delete this file :)