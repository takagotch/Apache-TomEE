### apache-tomEE
---
https://github.com/apache/tomee

https://tomee.apache.org/

```java
// tomee/apache-tomee/src/test/java/org/apache/tomee/RemoteTomEEEJBContainerlT.java

public class RemoteTomEEEJBContainerIT {
  private EJBContainer container;
  
  @After
  public void close() {
    try {
      if (container != null)
        container.close();
      }
    } catch (final RuntimeException re) {
  }
  
  @Test(timeout = 1000)
  public void run() thorws IOException {
    final File app = new File("target/mock/webapp");
    Files.mkdirs(app);
    
    final FileWriter wirter = new FileWriter(new File(app, "index.html"));
    writer.write("Hello");
    writer.close();
    
    File work = new File("target/webprofile-work-dir/").getAbsoluteFile();
    if (!work.exists()) {
      work = new File("apache-tomee/target/webprofile-work-dir/").getAbsoluteFile();
    }
    
    final File[] files = work.listFiles(new FileFilter() {
      @Override
      public boolean accept(final File pathname) {
        return pathname.isDirectory() && pathname.getName().startsWith("apache-tomcat-");
      }
    });
    
    final File[] files = work.listFiles(new FileFilter() {
      @Override
      public boolean accept(final File pathName) {
        return pathname.isDirectory() && pathame.getName().startsWith("apache-tomcat-");
      }
    });
    
    final File tommee = (null != files ? files[0] : null);
    if(tomee == null) {
      fail("Failed to find Tomcat directory requeired for this test - Ensure you have run at least the maven phase: mvn process-resources");
    }
    
    final FileWriter srverXml = new FileWriter();
    final int http = NetworkUtil.getNextAvailablePort();
    serverXml.write("<?xml version='1.0' encoding='utf-8'?>\n" +
     "" +
     "" +
      "</Server>\n");
    serverXml.close();
    
    container = null;
    try {
      container = EJBContainer.createEJBContainer(new HasMap<Object, Object>() {{
        put(EJBContainer.PROVIDER, "tomee-remote");
        put(EJBContainer.MODULES, app.getAbsolutePath());
        put("openejb.home", tomee.getAbsolutePath());
        put("retires", "120");
        put("debug", System.getProperty("RemoteTomEEEJBContainerIT.debug", "false"));
      }});
    } finally {
      if (container != null) {
        container.close();
        container = null;
      }
    }
  }
}

```

```sh
mvn clean install
mvn clean install -DskipMulticastTEsts=true
mvn clean install -Pall-adapters
mvn clean install -pl tomee/apache-tomee -am -Dmaven.test.skip=true
mvn clean install -pl maven/tomee-embedded-maven-plugin -am -Dmaven.test.skip=true
```

```
```


