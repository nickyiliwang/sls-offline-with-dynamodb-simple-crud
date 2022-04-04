# simple_CRUD_DDB
Simple dynamodb database with CRUD

Installation:
```
1. add plugins in yaml and npm install
plugins:
  - serverless-dynamodb-local
  - serverless-offline

2. add custom settings in yaml
  dynamodb:
      stages:
          - dev
      start:
          port: 8000
          inMemory: true
          migrate: true
      migration:
          dir: offline/migrations

3. make the migration file in offline/migrations/***.json

This is the contents in ddb.json as an example mirroring our yaml file:
{
  "Table": {
    "TableName": "posts",
    "keySchema": [
      {
        "AttributeName": "id",
        "KeyType": "HASH"
      }
    ],
    "AttributeDefinitions": [
      {
        "AttributeName": "id",
        "AttributeType": "S"
      }
    ],
    "ProvisionedThroughput": {
      "ReadCapacityUnits": 1,
      "WriteCapacityUnits": 1
    }
  }
}

4. add the config where ever the DocumentClient is used

const db = new AWS.DynamoDB.DocumentClient({
  region: "localhost",
  endpoint: "http://localhost:8000",
});

5. run: <sls dynamodb install> and make sure you have the Java SE Development Kit for the DDB engine

6. sls offline start and test your setup
```

Credits:
1. [CRUD post repo](https://github.com/hidjou/classsed-lambda-dynamodb-api)
2. [offline ddb setup tutorial](https://www.youtube.com/watch?v=ul_85jfM0oo)