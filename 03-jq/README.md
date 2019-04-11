# jq

[`jq`](https://stedolan.github.io/jq/manual/) is a tool to parse and transform `json` files. It's really versatile tool.

>        jq  can  transform  JSON in various ways, by selecting, iterating, reducing and otherwise mangling JSON documents. For instance, running the command jq 'map(.price) | add' will
>       take an array of JSON objects as input and return the sum of their "price" fields.
>
>       jq can accept text input as well, but by default, jq reads a stream of JSON entities (including numbers and other literals) from stdin. Whitespace is only  needed  to  separate
>       entities such as 1 and 2, and true and false. One or more files may be specified, in which case jq will read input from those instead. 


In this directory is file `countries.json` which we will be using throught this tutorial.

It's pretty big so it's best to pipe it to `less`.  
`jq . countries.json | less`

## Finding items

We can use `jq` to access items in our `json`.  

- **Get one item `.[NTH]`**  
    `cat countries.json | jq '.[100].name'`  
    Output: `Honduras`  

- **It's also possible to get slices of data `.[NTH:MTH]`**  
    `cat countries.json | jq -c '.[101:102][] | .name'`  
    Output: `Hong Kong`

- **Searching for `key` with specific value. In our case we look for country *Sweden* ` select(.KEY=="VALUE")`**  
    `cat countries.json | jq  '.[] | select(.name=="Sweden") | .capital'`  
    Output: `Stockholm`

## Manipulating and transforming json

`jq` is able to transform data into new defined structure, removing fields, renaming fields, etc

- **Create array with data that is interesting to us like `name`, `capital`, `nativeName` and german translation**  
    `cat countries.json | jq -c  '.[] | [.name, .capital, .nativeName, .translations.de]' | head -n1`  
    Output: `["Afghanistan","Kabul","افغانستان","Afghanistan"]`
    
    *Note: `-c` is to display output in one line*