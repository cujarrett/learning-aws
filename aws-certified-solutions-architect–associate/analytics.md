# Analytics

## Kinesis
Amazon Kinesis is a platform on AWS to send your streaming data to. Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for your business needs.

### Kinesis Types
- #### Kinesis Streams
    Amazon Kinesis Data Streams is a scalable and durable real-time data streaming service that can continuously capture gigabytes of data per second from hundreds of thousands of sources.
    ![Kinesis Streams info](https://user-images.githubusercontent.com/16245634/71392569-12601980-25ce-11ea-846a-18ecd2c383ca.png)
    _image from [A Cloud Guru](https://acloud.guru/)_
    
    - Stored for 24 hours up to a maximum of 7 days
    
    Kinesis Streams Consists of Shards
    - 5 transactions per second for reads, up to a maximum total data read rate of 2MB per second and up to 1,000 records per secind for writes, up to a maximum total data write of 1MB per second (including partition keys).
    - The data capacity of your stream is a function of the number of shards that you specify for the stream. The total capacity of the stream is the sum of the capacities of its shards.

- #### Kinesis Firehose
    Amazon Kinesis Data Firehose is the easiest way to capture, transform, and load data streams into AWS data stores for near real-time analytics with existing business intelligence tools.
    ![Kinesis Firehose info](https://user-images.githubusercontent.com/16245634/71392869-64556f00-25cf-11ea-9cc5-d9b74d8cce35.png)
    _image from [A Cloud Guru](https://acloud.guru/)_

    - Data is not persisted, you must do something with it

- #### Kinesis Analytics
    Amazon Kinesis Data Analytics is the easiest way to process data streams in real time with SQL or Java without having to learn new programming languages or processing frameworks.
    ![Kinesis Analytics info](https://user-images.githubusercontent.com/16245634/71393014-12611900-25d0-11ea-8cc1-b843e2cff429.png)
    _image from [A Cloud Guru](https://acloud.guru/)_
     
### What is Streaming Data?
Streaming Data is data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously, and in small sizes (order of Kilobytes).

Examples:
- Purchases from online stores (think amazon.com)
- Stock prices
- Game data (as the player plays)
- Social network data
- Geospatial data (think uber.com)
- iOT sensor data (think farm data streaming in from devices)
