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
