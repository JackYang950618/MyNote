//根据外部Url 来获取数据
 public static String getURLContent(String urlStr) {

        //请求的url
        URL url = null;

        //建立的http链接
        HttpURLConnection httpConn = null;

        //请求的输入流
        BufferedReader in = null;

        //输入流的缓冲
        StringBuffer sb = new StringBuffer();

        try{
            url = new URL(urlStr);

            in = new BufferedReader(new InputStreamReader(url.openStream(),"UTF-8") );

            String str = null;

            //一行一行进行读入
            while((str = in.readLine()) != null) {
                sb.append( str );
            }
        } catch (Exception ex) {

        } finally{
            try{
                if(in!=null) {
                    in.close(); //关闭流
                }
            }catch(IOException ex) {

            }
        }
        String result =sb.toString();
        return result;
    }
		
		/*将请求的数据返回成JSONObject*/
    public static JSONObject getJSONObject(String urlStr){

        String result=getURLContent(urlStr);
        JSONObject jsonObject=JSONObject.fromObject(result);

        return jsonObject;

    }
    
    //向指定url传输数据
    
    import org.apache.http.HttpResponse;
import org.apache.http.HttpStatus;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
/**客户端***/
public class Connect {
    /*推送信息到云平台接口*/
    public static  void postMessage(String url,String json) throws IOException {

        HttpClient httpclient = HttpClients.createDefault();
        HttpPost httppost = new HttpPost(url);
        httppost.addHeader("Content-Type", "application/json; charset=utf-8");
        //构建一个json格式字符串textMsg，其内容是接收方需要的参数和消息内容
        String textMsg = json;
        StringEntity se = new StringEntity(textMsg, "utf-8");
        httppost.setEntity(se);
        HttpResponse response = httpclient.execute(httppost);
        if (response.getStatusLine().getStatusCode() == HttpStatus.SC_OK) {
            String result = EntityUtils.toString(response.getEntity(), "utf-8");
            System.out.println(result);
        }

    }
}
/**服务器端***/
public void Test(ServletRequest request, ServletResponse response){
            StringBuffer str = new StringBuffer();
            BufferedReader reader=null;
            reader = new BufferedReader(new InputStreamReader(request.getInputStream(),"UTF-8"));
	    String string=null;
	    if((string=reader.readLine()!=null)){
	      str.append(string);
	    }
	    String string = new String(str);//从客户端传输的数据
}
    
    
    
    import com.alibaba.fastjson.JSON;
    //已知json字符串 获取属性
       String json="{\"name\":\"YH\",\"age\":\"24\"}";
       JSONObject jsonObject=getJSONObject1(json);
       String name=json.get("name");==>YH
       String age=json.get("age");==>24
       
       
	 获取当前网页的地址（服务器也适用）
  return window.location.pathname.replace("/","").replace(项目名称,"").replace("/","");
