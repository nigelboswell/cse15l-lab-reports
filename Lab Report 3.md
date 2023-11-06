# CSE 15L Lab Report 3

**Failure Inducing input**
```
@Test
public void 1() throws URISyntaxException, IOException {
    Handler h = new Handler("./technical/");
    URI nullPath = new URI("http://localhost");
    assertNull(h.handleRequest(nullPath));
}
```

**Input that** *Doesnt* **induce a failure**
```
@Test
public void test2() throws URISyntaxException, IOException {
    Handler h = new Handler("./technical/");
    URI validPath = new URI("http://localhost/");
    assertNotNull(h.handleRequest(validPath));
}
```
**The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)**

I couldn't get my junit import to my server testing .java file to stop failing so I couldn't actually run it as a junit test, I will likely have to come into office hours for this.

**The bug causing code**
```
if (url.getPath().equals("/")) {
           return String.format("There are %d total files to search.", paths.size());
}
```
**The Fixed code**
```
if (url.getPath() != null && url.getPath().equals("/")) {
           return String.format("There are %d total files to search.", paths.size());
}
```
## Part 2
