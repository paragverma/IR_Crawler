# Drupal Module for Fetching Search Results from ElasticSearch instead of Drupal DB

## Documentation for Elasticsearch Module

### Installation Instructions
1. Install Drupal 7.x
2. Copy 'elasticsearch' folder to *root*/sites/all/modules
3. Log in to Drupal as an administrator
4. Go to modules page and activate 'Elasticsearch' module
5. Go to Configuaration -> Search Settings and Activate Elasticsearch as a Search Module
6. Also set it as the default search module

### elasticsearch.module
-elasticsearch_menu()
-mylog($logstring)
-search_it($query)
-perform_search()
-elasticsearch_search_execute($keys = NULL, $conditions = NULL)
-elasticsearch_search_info()

#### elasticsearch_menu()

This is the Drupal Hook which registers `hostname`/elasticsearch/search as a route in the Drupal ecosystem.
It returns an array containing the title, path, permissions, callback function and callback type associated with this route.
Currently, it registers `hostname`/elasticsearch/search as a route which is visible on the Navigation Bar of any user.

#### mylog($logstring)

A logging utlity which logs into a file named `log.txt` in the Elasticsearch module folder. This function can be used in other modules as well.

#### search_it($query)

This function takes a string argument and returns a JSON formatted string. The argument string is sent as a query to the Elasticsearch instance. The parameters for the ES instance are `host`http://localhost:9200 `credentials` elastic:changeme `method` POST.

####elasticsearch_search_execute($keys = NULL, $conditions = NULL)####

This is the Drupal hook for the event `search execute`. This function runs when a user has entered a query in the search box and pressed the search button. $keys is the user query, which is a string. $conditions are filters which a user applies when using advanced search.

This function calls the `search_it` function to get the results from the ES store. It then conforms the data according to Drupal's rules of formatting search results.
The fields 'link','type', 'title', 'user', 'date, 'node, 'extra', 'score', 'snippet' are required by Drupal as essential fields of a valid search result and thus they are set, either with a value from ES store or NULL.

####elasticsearch_search_info()####

This is the Drupal hook which registers the current module as a `Active Search Module` and allows replacing of default search results with our own, as long as they are in a valid format, as explained above.





