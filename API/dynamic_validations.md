### Dynamic Response Based on Payload

WireMock can return different responses based on request content.


Request Matching:  Stub 1:

```java
stubFor(post(urlEqualTo("/customer")).withRequestBody(matchingJsonPath("$.customerType", equalTo("PREMIUM")))
			.willReturn(okJson("""
						{
						   "discount":20
						}
						""")));
```

Another Stub (2):

```java
stubFor(post(urlEqualTo("/customer")).withRequestBody(matchingJsonPath("$.customerType",equalTo("REGULAR")))
    .willReturn(
        okJson("""
        {
           "discount":5
        }
        """)));
```

### Testing Internal Routing Logic

A very important validation is:

```text
Input Payload
      |
      v
Correct Internal API Called?
```

**Example**:
```java
verify(1,postRequestedFor(urlEqualTo("/premium/customer")));

verify(0,postRequestedFor(urlEqualTo("/regular/customer")));
```

This proves your routing logic works correctly.


