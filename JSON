**取得 json 文字檔內容
解析 json 陣列物件
放入 HashMap
放入 ArrayList
和 Listviwe 做資料配接**

{ "works": [{ "work_id": "2014101603", "size1": 165 }, { "work_id": "2014101602", "size1": 45 }] }

二種方式 讀取assets資料夾的檔案
```java
String result = "";
byte[] buffer;
//方式一
try {
			InputStream inpSt = getAssets().open("works.txt");
			int size = inpSt.available();
			buffer = new byte[size];
			inpSt.read(buffer);
			result = new String(buffer);
			inpSt.close();

		} catch (IOException e) {
			Log.e("Ch08GetIntSto", e.toString());
		}

//方式二
protected void readJSON() {
try {			
			InputStream inpSt = getAssets().open("works.txt");

			BufferedReader reader = new BufferedReader(new InputStreamReader(
					inpSt, "iso-8859-1"), 8);

			StringBuilder sb = new StringBuilder();
			String line = null;
			while ((line = reader.readLine()) != null) {
				sb.append(line + "\n");
			}
			result = sb.toString();
			inpSt.close();

		} catch (IOException e) {
			Log.e("Ch08GetIntSto", e.toString());
		}
}    
```
<hr>
使用http的方式取得json資料
```java
InputStream is = null;	
String result = "";
//這一段要放在AsyncTask中執行
	private String getJSON() {
//取得InputStream
		try {
			String url = "http://192.168.0.104/android_connect/get_golds.php";		
			 HttpClient httpclient = new DefaultHttpClient();
			 HttpPost httppost = new HttpPost(url);//	HttpGet httpGet = new HttpGet(url);
			 HttpResponse response = httpclient.execute(httppost);//HttpResponse response = httpClient.execute(httpGet);			
			 is = entity.getContent();
			HttpEntity httpEntity = response.getEntity();
			is = httpEntity.getContent();
		} catch (Exception e) {
			Log.e("log_tag", "Error in http connection " + e.toString());
		}
    
    //InputStream轉成字串
    try {
			BufferedReader reader = new BufferedReader(new InputStreamReader(
					is, "iso-8859-1"), 8);
			StringBuilder sb = new StringBuilder();
			String line = null;
			while ((line = reader.readLine()) != null) {
				sb.append(line + "\n");
			}
			is.close();
			result = sb.toString();
		} catch (Exception e) {
			Log.e("log_tag", "Error converting result " + e.toString());
		}
		return result;
}


class LoadData extends AsyncTask<Void, Void, Void> {
		@Override
		protected Void doInBackground(Void... params) {
			mydata = getJSON();
			return null;
		}

		@Override
		protected void onPostExecute(Void args) {
			tvIntro.setText(mydata);
		}
	}
  
@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		new LoadData().execute();
}    

```

<hr>
```java
ArrayList<HashMap<String, String>> arraylist= new ArrayList<HashMap<String, String>>();
ListView lv = (ListView) findViewById(R.id.lvWorks);
String json= readJSON();
JSONObject obj=new JSONObject(json);
JSONArray array=obj.getJSONArray("works");
for(int i=0;i<array.length;i++){
	HashMap<String, String> map = new HashMap<String, String>();
				JSONObject c = array.getJSONObject(i);// 取得陣列物件
				map.put("size1", c.getString("size1"));// 取得陣列物件中名為size1的值,指定給map物件
				map.put("work_id", c.getString("work_id"));
				arraylist.add(map);
}
```

```java
ListAdapter adapter = new SimpleAdapter(this, arraylist,
				R.layout.list_item, new String[] { "work_id", "size1" },
				new int[] { R.id.tvWorkId, R.id.tvSize1 });
		lv.setAdapter(adapter);
```    
