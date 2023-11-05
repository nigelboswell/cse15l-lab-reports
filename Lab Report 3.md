# CSE 15L Lab Report 3

**Failure Inducing input**
```
{
@Test
public void testBugCase() throws URISyntaxException, IOException {
    Handler h = new Handler("./technical/");
    URI rootPath = new URI("http://localhost/search?q=non-existent-term");
    String expect = "Found 0 paths:";
    assertEquals(expect, h.handleRequest(rootPath));
}
}
```
