package com.ko_dr_sol.fundquery;





import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLConnection;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ExecutionException;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

import android.os.AsyncTask;
import android.util.Log;


public class Methods {
	
	
	
	//List<String> fundnameDownload=new ArrayList<String>(500);//基金名字網頁下載資料
	String[] fundnameDownload=new String[2000];//基金名字網頁下載資料
	List<String> fundname=new ArrayList<>(500);//基金名字
	//String[] fundname=new String[2000];//基金名字
	//List<String> fundCouponDownload=new ArrayList<String>(500);//基金配息網頁下載資料
	String[] fundCouponDownload=new String[2000];//基金配息網頁下載資料
	List<String> fundCoupon=new ArrayList<>(500) ;//基金配息
	//String[] fundCoupon=new String[2000] ;//基金配息
	int CouponVariables=0;//配息變數
	int nameVariables=0;//基金變數
	int nameVariablesDownload=0;//基金變數下載
	MainActivity m;
	Double one=5.0;
	Double tow=10.0;
	
	

	public void connection(){
		
		try {
			new AsyncTask<Void, Void,String[]>() {

				@Override
				protected String[] doInBackground(Void... params) {
					String urlString = "http://www.moneydj.com/funddj/yp/YP700000.djhtm?S0=all&S1=&S7=&S3=%AC%FC%A4%B8&S2=&S4=500&S9=&S5=2";
					HttpURLConnection connect;
					
						URL url;
						try {
							url = new URL(urlString);
							URLConnection URLConn = url.openConnection();
							URLConn.setRequestProperty("User-agent", "IE/6.0");
							InputStream is = URLConn.getInputStream();					
							Document doc = Jsoup.parse(is, "big5", urlString);
							// 取得標頭					
							//fundnameDownload.add(doc.select("td[myClass]").select("a").append(",").text().split(",").toString())  ;
							fundnameDownload=doc.select("td[myClass]").select("a").append(",").text().split(",");
							//fundCouponDownload.add(doc.select("td[nowrap]").append(",").text().split(",").toString());
							//fundCouponDownload=doc.select("td[nowrap]").append(",").text().split(",");
							
						} catch (MalformedURLException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						} catch (IOException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
						
						
						
						
						return fundnameDownload;
			
				}
					
					@Override
					protected void onPostExecute(String[] hotspotList) {
						//couponscreening();//配息篩選
						
					}
			}.execute().get();
		} catch ( Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		}
	
	
	
public void connection2(){
		
		try {
			new AsyncTask<Void, Void,String[]>() {

				@Override
				protected String[] doInBackground(Void... params) {
					String urlString = "http://www.moneydj.com/funddj/yp/YP700000.djhtm?S0=all&S1=&S7=&S3=%AC%FC%A4%B8&S2=&S4=500&S9=&S5=2";
					HttpURLConnection connect;
					
						URL url;
						try {
							url = new URL(urlString);
							URLConnection URLConn = url.openConnection();
							URLConn.setRequestProperty("User-agent", "IE/6.0");
							InputStream is = URLConn.getInputStream();					
							Document doc = Jsoup.parse(is, "big5", urlString);
							// 取得標頭					
							//fundnameDownload.add(doc.select("td[myClass]").select("a").append(",").text().split(",").toString())  ;
							//fundnameDownload=doc.select("td[myClass]").select("a").append(",").text().split(",");
							//fundCouponDownload.add(doc.select("td[nowrap]").append(",").text().split(",").toString());
							fundCouponDownload=doc.select("td[nowrap]").append(",").text().split(",");
							
						} catch (MalformedURLException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						} catch (IOException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
						
						
						
						
						return fundCouponDownload;
			
				}
					
					@Override
					protected void onPostExecute(String[] hotspotList) {
						//couponscreening();//配息篩選
						
					}
			}.execute().get();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		}

	//配息篩選
	public void couponscreening(){
		
			
		
	
		//for(int f=3;f<=fundCouponDownload.size();f+=5){//基金配息網頁下載資料長度
		for(int f=3;f<=fundCouponDownload.length;f+=5){//基金配息網頁下載資料長度
			//if(fundCouponDownload.get(f).trim().equals("N/A")){//基金配息網頁下載,去掉N/A
			if(fundCouponDownload[f].trim().equals("N/A")){//基金配息網頁下載,去掉N/A
				continue;
			}else{
				
				//Log.e("aa", fundCouponDownload.get(f));
				Log.e("aa", fundCouponDownload[f]);
				//if((Double.parseDouble(fundCouponDownload[f].toString()))>5.0){//基金配息>5找出來	
				if((Double.parseDouble(fundCouponDownload[f].toString()))>one&&(Double.parseDouble(fundCouponDownload[f].toString()))<tow){//基金配息>5找出來
				
					//fundCoupon[CouponVariables++]=fundCouponDownload[f];       ////基金名字>5,設到集合出
					//fundCoupon.add(fundCouponDownload.get(f));       ////基金名字>5,設到集合出
					//fundCoupon.add(fundCouponDownload[f]);       ////基金名字>5,設到集合出
					fundCoupon.add(CouponVariables++, fundCouponDownload[f]);
					//fundname[nameVariables++]=fundnameDownload[nameVariablesDownload];//基金配息>5
					//fundname.add(fundnameDownload.get(nameVariablesDownload));           //基金配息>5
					//fundname.add(fundnameDownload[nameVariablesDownload]);           //基金配息>5
					fundname.add(nameVariables++,fundnameDownload[nameVariablesDownload]);
			}
				nameVariablesDownload++;
			}			
		
		}			
	}
}






