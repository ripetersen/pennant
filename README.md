# pennant
Pennant is a feature flag and configuration management system.  

## pennant features
* easily understood : Pennant provides a high performance distributed key value mapping, where the key is a (optionally) a user, an environment, and a named "feature"
* feature publishing : Clients can subscribe to have added/changed values pushed to them, there by updating the runtime state of the client
* rich types : values are any valid JSON representation, allowing not only a `true` or `false` but arbitrary complex representations of a feature value.
* dynamic assignment : The value of a feature can be randomly generated.  For example a `true`/`false` value can be assigned an 80% / 20% probability
* calculated/categorical assignement : When requesting a value in addition to the `key` a `profile` can be provided which is used in the determination of a value, e.g.
 ```
 { 
    groups = ['foo', 'bar', 'beta1']
 }
 ```
 Can be evaluated against a JSON schema expression such as :
 ```

  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "group": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "contains": {
        "const": "beta1"
      }
    }
  },
  "required": ["group"]
}
```
the JSON schema is pared with a probability and value, e.g. 
```
{
 70: true,
 30: false,
}
```
(keys of the probability map are normalized to sum to 1.0)
* cached results: the value of a dynamic/calculated key can be stored for a given `user`, and/or `environment`, and `key` tuple
* scheduled publishing : publishing new/updated feature flags can be scheduled
* state dependant publishing : publishing new/updated features can be made dependent of the value/state of an external system


 
