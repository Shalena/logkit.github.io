{% case include.family %}

{% when 1.0 or 1.1 %}


The HTTP JSON Endpoint is hard-coded to include a special `entryFormatter` that converts each [Log Entry][entries] to a dictionary, then [JSON][json] serializes it for upload. This formatter includes all [properties of a Log Entry][entries], including the Entry's [`userInfo`][entry-props]. Each Log Entry property becomes a top-level item in the dictionary. Any top-level items in an Entry's `userInfo` will become top-level items with the rest of an Entry's properties. Dictionary key conflicts between `userInfo`'s items and an Entry's properties will result in `userInfo`'s conflicted items being overwritten by the Entry's items. Developer beware.

It is the application developer's duty to ensure that all [`userInfo`][entry-props] items are JSON-serializable if this [Endpoint][endpoints] is in use. A non-JSON-serializable item will cause the Log Entry to be skipped in a shipping application (though in a test build, the application will abort).


{% else %}


The HTTP JSON Endpoint is hard-coded to include a special `entryFormatter` that converts each [Log Entry][entries] to a dictionary, then [JSON][json] serializes it for upload. This formatter includes all [properties of a Log Entry][entries], including the Entry's [`userInfo`][entry-props]. Each Log Entry property becomes a top-level item in the dictionary, including `userInfo`. `userInfo` items, therefore, are located in a sub-dictionary under the `userInfo` key.

> Note: The behavior for serializing `userInfo` described above is a change from LogKit 1. Developer beware.

It is the application developer's duty to ensure that all [`userInfo`][entry-props] items are JSON-serializable if this [Endpoint][endpoints] is in use. A non-JSON-serializable item will cause the Log Entry to be skipped in a shipping application (though in a test build, the application will abort).

Additionally, the HTTP JSON Endpoint includes the `LXDateFormatter.ISO8601DateTimeFormatter()` [date formatter][date-formatting] as its default `dateFormatter`. This is a different default than other [Endpoints][endpoints] include.

Here is an example [Log Entry][entries] serialized to [JSON][json] (not all properties are shown for brevity):

{% highlight json %}
{
    "message": "Hello Internet!",
    "userInfo": {
        "my_property": 1,
        "other_property": 2,
    },
    "dateTime": "2015-10-06T02:44:21.112000Z",
    "timestamp": 1444099461.112487,
    "level": "Debug",
    ...
}
{% endhighlight %}


{% endcase %}
