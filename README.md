
Gradle
```
compile 'thaithien:SimpleNeo4jManager:0.2'
```

Maven
```
<dependency>
  <groupId>thaithien</groupId>
  <artifactId>SimpleNeo4jManager</artifactId>
  <version>0.2</version>
  <type>pom</type>
</dependency>
```


Simple usage : see junit test


```
package SimpleNeo4j;

import org.junit.Test;

import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

import static org.junit.Assert.*;

public class Neo4jManagerTest {

    @Test
    public void query() throws Exception {
        Neo4jManager.initialDriver("localhost", "7687", "neo4j", "meowmeow");

        DateFormat df = new SimpleDateFormat("MMddyyyyHHmmss");

        Date today = Calendar.getInstance().getTime();

        String reportDate = df.format(today);


        System.out.println("Report Date: " + reportDate);
        String q = String.format("CREATE (t:TEST{name:'%s', testOk:'OK'}) return t", reportDate);
        System.out.println("test query");
        Neo4jManager.query(q).forEach(x->{
            String date = x.get("t.name");
            System.out.println(date);
            String testOk = x.get("t.testOk");
            assert (testOk.equals("OK"));
            assert (date.equals(reportDate));
        });
    }
}
```