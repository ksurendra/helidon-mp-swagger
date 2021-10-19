# Helidon MP With Swagger Example

Sample Helidon MP project with Swagger / OpenAPI.

Built a new project using Helidon MP 2.3.4 
```xml
mvn -U archetype:generate -DinteractiveMode=false \
    -DarchetypeGroupId=io.helidon.archetypes \
    -DarchetypeArtifactId=helidon-quickstart-mp \
    -DarchetypeVersion=2.3.4 \
    -DgroupId=io.helidon.examples \
    -DartifactId=helidon-mp-swagger \
    -Dpackage=io.helidon.examples.mp.swagger
```

## Build and run

With JDK11+
```bash
mvn package
java -jar target/helidon-mp-swagger.jar
```

## Using the example

Sample Open API details are added to the class `src/main/java/io/helidon/examples/mp/swagger/GreetResource.java` as:

```java
 @Path("/greeting")
    @PUT
    @Consumes(MediaType.APPLICATION_JSON)
    @Produces(MediaType.APPLICATION_JSON)
    @RequestBody(name = "greeting",
            required = true,
            content = @Content(mediaType = "application/json",
                    schema = @Schema(type = SchemaType.STRING, example = "{\"greeting\" : \"Hola\"}")))
    @APIResponses({
            @APIResponse(name = "normal", responseCode = "204", description = "Greeting updated"),
            @APIResponse(name = "missing 'greeting'", responseCode = "400",
                    description = "JSON did not contain setting for 'greeting'")})
    public Response updateGreeting(JsonObject jsonObject) { ... }
```

Use the below URL to see the API details, like in Swagger-UI:
```
http://localhost:9393:8080/openapi-ui/index.html
```
![helidon-mp-swagger-screenshot](https://user-images.githubusercontent.com/902972/137933830-05db4fca-b8ba-48ae-9104-c1b4c8795b5b.png)

### Known issue
1. The url redirects/maps to `http://[::1]:8080/openapi-ui/index.html` 