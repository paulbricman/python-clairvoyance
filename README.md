# Clairvoyance
Modular microframework which performs some basic data mining by generating directed graphs through a number of transforms. It works mostly by leveraging the power of third-party public APIs.

## Background
An open API (often referred to as a public API) is a publicly available application programming interface that provides developers with programmatic access to a proprietary software application or web service. Combining free public APIs from **data processing** services like Algorithmia, **social networks** like Twitter, **geolocators** like Google etc. results in a useful swiss army knife for data mining.

## Usage
After you import the `clairvoyance.core` and a transform package, you can create an instance of a graph and perform operations with it. Let's create an instance.
```
G = core.Graph()
```
Let's add a node in the graph, an entity called `Jane` entity of type `string`.
```
G.add_entity('Jane', 'string')
```
Now let's perform a `string_to_gender` transform.
```
G.make_transform(['Jane'], nlp_transforms.string_to_gender)
```
Now the graph should contain another node, which is connected with the initial node. Performing multiple operations we can reach this:
![Demo](https://github.com/paubric/python-clairvoyance/blob/master/Figure_2.png)

## Transforms
### Available Transforms
- **nlp_transforms.string_to_len** - Get length of string
- **nlp_transforms.string_to_word_count** - Get number of words from strings
- **nlp_transforms.string_to_gender** - Get gender of name
- **nlp_transforms.string_to_tags** - Get relevant tags from text
- **nlp_transforms.string_to_summary** - Get summarized version of text

A transform has the following structure and it can be easily integrated: 
```
def intype_to_outtype(graph, nodes):
    print('Performing transform string_to_len on nodes: ', nodes)

    input_type = 'intype'
    output_type = 'outtype'
    transform_results = []

    for node in nodes:
        if (graph.nodes[node]['type'] == input_type):
            transform_results.append(singular_transform(node))
        else:
            print('Incompatible types')
            return (-1, -1)

    return transform_results, output_type
```

## TODO
- code refactoring
- implement one-to-many node transforms
- more nlp_transforms: entity recognition, translation, identify language etc.
- social transforms: get tweets containing term, get last tweets of user etc.
- other transforms: geolocation, ip/domain lookup, dns records, face api etc.
- improve(implement) visualization
