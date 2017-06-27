```java
import org.apache.http.Header;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.fluent.Form;
import org.apache.http.client.fluent.Request;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.nio.charset.Charset;

/**
 * Created by maoxiangyi on 2017/6/26.
 */
public class EasyPost {
    public static void main(String[] args) throws IOException {
        HttpResponse response = Request.Post("http://shop.itcast.cn/login/login.html")
                .bodyForm(Form.form().add("username", "maoxiangyi").add("password", "maoxiangyi").add("reURL","http://shop.itcast.cn/item/itemList.html").build())
                .execute().returnResponse();
        if (response.getStatusLine().getStatusCode() == 302) {
            Header[] locations = response.getHeaders("Location");
            String url = locations[0].getValue();
            System.out.println(url);
            HttpGet httpGet = new HttpGet(url);
            String html =  Request.Get(url).execute().returnContent().asString(Charset.forName("UTF-8"));
            System.out.println(html);
        }
    }
}
```java