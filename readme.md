# Use Amplify Enterprise Marketplace to Identify Duplicate APIs

This code supports the article: [Art of the possible: reduce duplicate APIs with Amplify Enterprise Marketplace](https://blog.axway.com/product-insights/amplify-platform/enterprise-marketplace/reduce-duplicate-apis)

Setup:

1. Create a [Service Account](https://docs.axway.com/bundle/platform-management/page/docs/management_guide/organizations/managing_organizations/index.html#managing-service-accounts) which can retrieve the list of APIs from the Service Registry and fetch the associated API Specifications. Central Admin permissions will always work, but you may be able to use lesser depending on how permissions in the Marketplace have been configured.
2. In this example I use ClientId and ClientSecret to authenticate using the axway CLI. The ClientId and ClientSecret are stashed in a .env file. If you want to take a different approach to authenticating the CLI, modify the `collect-services.sh` script appropriately.

Execution:

1. Clone this repo
2. Modify `collect-services.sh` per the setup instructions above
3. Execute the `collect-services.sh` script. depending on the number of APIs in your Service Registry, this may take some time. The script will create two directories containing the list of discovered APIs and their related API Specifications.
4. Execute `compare.py` to run the comparison. It will use the API specifications stored in the apispecs folder, so it can be re-run without having to read the Service Registry every time.

If you want to referesh the known API specifications then delete the service-docs and api-services folders and run the `collect-services.sh` script again.

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
