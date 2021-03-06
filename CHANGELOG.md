# CHANGELOG

### 10-08-2018 Ben W.

Added in the scaffolding necessary to get "producer" side Spring Cloud Contracts in the Trader-App. This means that there are some changes to the Trader-App `POM.xml` and new API contract specifications written in Groovy. These specs are in the `/test/resources/contracts` folder and sre organised into folders by consumer. Each file contains a single spec of a request-response interaction. These contracts are used in two ways: firstly they are used by the SCC plugin to generate JUnit tests for the API specified (find them in `target/generated-test-sources`), and secondly a "stubs" jar is created which contains the specifications needed for wiremock to be able to fake the same API. To generate and run these contract-based tests use `mvn test` to add the stubs jar to your local `.m2` folder, use `mvn install`. 

> Side note: notice that the JUnit tests generated by SCC extend the same base class (`BaseContractTest`). This base class must be provided and is configured via the plugin XML configuration in the `POM.xml`.

Separated the Unit level tests from the Integration level tests (test that run SpringBoot, like `@SpringBootTest`, `@DataJpaTest`, `@WebMvcTest` etc.). This involved changes to the `POM.xml`. To benefit from this separation...

* Run unit tests > `mvn test`
* Run unit and integration tests > `mvn verify`