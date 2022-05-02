# High Level Notes for Python Script Investigation

### Notes From Jake
I got the guts of this written in about an hour this morning

pdp-arbor branch `feature/DATA-443/salesforce-staging-generator`

palm command: `palm salesforce-staging [MODEL_NAME]`

Run in `palm shell` with: `python3 scripts/salesforce_staging_generator [MODEL_NAME]`

Some work still to be done here including:  
- More logic in `SalesforceStagingGenerator.clean_label`  
- Apply some kind of sorting logic, ideally we want the ID first and the dbt_ columns last  
- better typecasting e.g. `TEXT` should be `VARCHAR`

I've also layed the groundwork for a test suite, including some failing tests!

To run the tests:  
`palm shell`  
`pytest scripts`

Please add more tests for any code that is added!

## Corey Python Notes
To continue from a `breakpoint()` type `continue`

with a dictionary, adding a value to a column name (e.g. `mappings[value]`) will map the keys in the dictionary

setting the key `mappings[value]` equal to a value will set the key value

Returning the keys from a dictionary is done by first converting the key view object to a list e.g. `map_keys = list(mappings.keys)` then printing with an index like `map_keys[0]` 

Do not forget to resuse labels when making consecutive transforms!!
```
# BAD!
clean_label = label.replace('whatever', 'w/e')
clean_label = label.replace('whatever', 'w/e')

# GOOD!
clean_label = label.replace('whatever', 'w/e')
clean_label = clean_label.replace('whatever', 'w/e')
```

