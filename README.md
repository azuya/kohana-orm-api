kohana-orm-api
===============

This module provides an api for fetching and manipulating ORM models over a 
[RESTful web API](https://en.wikipedia.org/wiki/REST#RESTful_web_APIs). 

The four HTTP methods GET, POST, PUT and DELETE are used (respectively) to 
find, create, update and delete models.

## Routing
The api is routed like this

    api/<model>(/<id>(/<action>))
    
If ```model``` is plural, a list of models will be returned in the JSON-encoded 
response body. The suffix ```_all``` will be appended to the called method to
perform a plural call.

As a default behiavior, the HTTP method is used to resolve the method to call on 
a model. Everything is therefore handled in the index action.

    GET is mapped to find
    PUT is mapped to create
    POST is mapped to update
    DELETE is mapped to delete

<action> is used to perform other operations such as has, add or remove.

## Querying
You may also sort, group and filter model using the HTTP query.

```json
{
    'where' => [
        ['column', 'operand', 'value']
    ],
    'having' => [
        ['column', 'operand', 'value']
    ],
    'group_by': 'column',
    'group_by': ['column_1', 'column_2'],
    'order_by': 'column',
    'order_by': ['column_1', 'column_2']
}
```

This is handy if you wish to alter the output of a plural call.

## Actions
This is a list of implemented actions

### Count
Count will count the number of entries matching the query.
count will return a JSON-encoded integer.

### Has, add and remove
A JSON object must be providen, containing

```json
    {
        'alias': <alias>,
        'far_keys': <far_keys>
    }
```

add and remove will return an empty body with a 200 status code on success.

has will return a JSON-encoded boolean.

### Check
Use the request body to update values in the model and then check its validity.

check will return an empty body with a 200 status code on success. JSON-encoded
errors will be returned on failure.

## Configuration
The only configuration required is a policy file that defines what columns and 
alias are available depending on the called method.

```php
return array(
    <policy> => array(
        <model> => array(
            <method> => array(
                'column_1', 'alias_1'
            )
        )
    )
);
```

## Usage/Examples

jQuery is well suited for the job when it comes to api-based website. You can create a nice app using its ajax implementation.

Note : since doing cross-browser compatible AJAX is an horrible task to do and since nobody does that anymore, we'll just assume in the following examples that you are using jQuery. It's a free (as in freedom) library that simplifies AJAX requests, along with every other thing raw javascript does and there is no excuse not to use it.

> You are going to put jQuery on your website, and that's final, young sir !

All complaints about that fact should be sent directly to /dev/null.


## Security

As the GNU licences say so well :

> This software is distributed in the hope that it will be useful,
> but WITHOUT ANY WARRANTY; without even the implied warranty of
> MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

This is an api that exposes your model in a generic manner, so do not take security concers with a grain of salt.

In a few words, we believe that this module is safe to use (when correctly configured), due to the simplicity of it's code, but be aware that we are humans and mistakes can always happen. Still, since this is a free project, you can always double-check the code yourself (or pay a developer to do it).

## License

Not decided yet. Comming soon :)

## In Conclusion

> And if you don't like the way we code, you can go fork yourself !
