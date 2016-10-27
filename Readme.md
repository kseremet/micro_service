# Logging solutions for Node.js
Here are some examples to start using some of the node.js logging API.


## Util Module

The important part here is how we expose the logger API and the need to stream to the stdout of our container, so OSE3 logging infrastructure [EFK](https://bitbucket.org/bankaudigroup/cesar-logging-infra) can gather the information and make them available for search through [Kibanna](https://www.elastic.co/products/kibana).

### Exposing the API

#### Dependencies

This example use a library called [sdiscovery](https://www.npmjs.com/package/sdiscovery) written by yours truly, is not obligatory to use, but I just use **whoami** method to get hostname and use this information to identify our microservice in the [node](https://docs.openshift.com/enterprise/3.0/admin_guide/manage_nodes.html).

#### getBunyanLogger

Handle the instanciation and configuration of [Bunyan](https://github.com/trentm/node-bunyan) Logger API, - *I prefer this one because is almost zero-configuration needed and ready to work*.  

#### getWinstonLogger

Handle the instanciation and configuration of [Winston](https://github.com/winstonjs/winston) Logger API. Less trivial but support more configurations.


#### Example

At the end in our code we consume this the following way:

```javascript

//util.js

module.exports = {
  ...
  Logger: getBunyanLogger(), // getWinstonLogger()
  ...
}

// usage

let logger = require('./lib/util').Logger;
logger.info('hello world');

// {"name":"host",
//"hostname":"vagrant-ubuntu-trusty-64",
// "pid":2090,"level":30,
//"msg":"hello world",
//"time":"2016-10-27T13:23:58.975Z","v":0}
```


[Application example](https://bitbucket.org/bankaudigroup/cesar-template).
