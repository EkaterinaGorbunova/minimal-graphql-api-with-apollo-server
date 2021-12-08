## [Minimal GraphQL API example with Apollo Server](https://www.preciouschicken.com/blog/posts/minimal-graphql-apollo-server/)

1. ```mkdir minimal-graphql-apollo-server```
2. ```cd minimal-graphql-apollo-server```
3. ```npm init -y```
4. ```npm install apollo-server graphql```
5. add 

    `index.js` -  is responsible for the server itself

    `db.json` - data to query

    `schema.js` (schema and resolvers, referred to as `typeDefs`) - defines the objects the queries will be calling and includes what types make up the object

6. Start the server
    ```bash
    npx nodemon index.js
    ```
    your code will be monitored and the server will restart automatically. Will save you lots of time if you are making frequent changes.

7. Test API

    ### Playground

    Below the statement #Write your query or mutation here enter the following query:
    ```bash 
    {
    beasts {
        commonName
        legs
    }
    }
    ```

    ### Arguments

    The `resolvers` we have built also allow us to supply arguments to define our search, so entering:

    ```bash
    {
    beast(id: "cc") {
        commonName
        taxClass
    }
    }
    ```

    ### Query variables

    Using our API for real we will likely not be hardcoding an argument directly into the query so the Query Variables section of the playground allows us to add variables in a similar way as to how we might via a web page (e.g. a form). To use this enter in the main query section:

    ```bash
    query($input: String!) {
    calledBy(commonName: $input) {
        binomial
        legs
    }
    }
    ```

    then in the Query variables field found at the bottom of the browser window enter the variable as so:

    ```bash
    {"input": "housefly"}
    ```

    ### Mutations

    So far we have just been querying the data, we can also amend it via a mutation.

    Our data set is missing some information; the old woman who has eaten all of these creatures. Therefore in the playground enter:

    ```bash
    mutation {
    createBeast(
        id: "hs"
        legs: 2
        binomial: "Homo sapiens"
        commonName: "old woman"
        taxClass: "Mammalia"
        eats: ["md", "nr", "cc", "fc"]
    ) {
        commonName
        eats {
        commonName
        }
    }
    }
    ```