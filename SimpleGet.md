```java
import org.apache.http.HttpEntity;
import org.apache.http.NameValuePair;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.nio.charset.Charset;
import java.util.ArrayList;
import java.util.List;

/**
 * Created by maoxiangyi on 2017/6/26.
 */
public class SimpleGet {
    public static void main(String[] args) throws Exception {
        CloseableHttpClient httpclient = HttpClients.createDefault();
        HttpGet httpGet = new HttpGet("http://sspc.itcast.cn");
        CloseableHttpResponse response = httpclient.execute(httpGet);
        System.out.println(response.getStatusLine());
        if (response.getStatusLine().getStatusCode() == 200) {
            HttpEntity entity = response.getEntity();
            String html = EntityUtils.toString(entity, Charset.forName("utf-8"));
            System.out.println(html);
        }
        response.close();
    }
}
```java