# Use Amplify Enterprise Marketplace to Compare API Specification

This code supports the article: [Art of the possible: reduce duplicate APIs with Amplify Enterprise Marketplace](https://blog.axway.com/product-insights/amplify-platform/enterprise-marketplace/reduce-duplicate-apis)

Setup:

1. Create a [Service Account](https://docs.axway.com/bundle/platform-management/page/docs/management_guide/organizations/managing_organizations/index.html#managing-service-accounts) which can retrieve the list of APIs from the Service Registry and fetch the associated API Specifications. Central Admin permissions will always work, but you may be able to use lesser depending on how permissions in the Marketplace have been configured.
2. In this example I use ClientId and ClientSecret to authenticate using the axway CLI. The ClientId and ClientSecret are stashed in a .env file. If you want to take a different approach to authenticating the CLI, modify the `collect-services.sh` script appropriately.

Execution:

1. Clone this repo
2. Modify `collect-services.sh` per the setup instructions above
3. Execute the `collect-services.sh` script. depending on the number of APIs in your Service Registry, this may take some time. The script will create two directories containing the list of discovered APIs and their related API Specifications.

If you want to referesh the known API specifications then delete the service-docs and api-services folders and run the `collect-services.sh` script again.

## Use cases
### Search for Similar APIs

Execute `compare.py` to run the comparison using the API specifications stored in the apispecs folder. This will generate a heat map depicting the relative similarities of all discovered APIs.

### Suggest API Asset groupings

Execute `compareSchemas.py` to run the comparison using the API specifications stored in the apispecs folder. This will compare the "schemas" section in the discovered specifications and look for similarities. This example will suggest grouping all APIs which potentially deal with the same data. The code can be adjusted to compare different attributes by modifying the appropriate section to look for the attribute you are interested in.

~~~
with open(os.path.join(directory, filename), 'r') as file:
                spec = json.load(file)
                # Extract and preprocess the schema section
                schema_section = json.dumps(spec.get("components", {}).get("schemas", {}), sort_keys=True)
                specs[filename] = schema_section
~~~

## Notes

Your python environment must contain the libraries for:
* numpy
* pandas
* seaborn
* matplotlib
* sklearn

Notes on the sample code:

|Variable|Usage|
|---|---|
|`cut_off`| Lowest value match to display in ouput. Default 0.7 will only display matches >= 70% |

To customize the heatmap refer to the [seaborn heatmap documentation](https://seaborn.pydata.org/generated/seaborn.heatmap.html).
