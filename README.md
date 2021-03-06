This is a scrapy spider to get "Stock Connect Northbound/Southbound from HKEXNEWS [滬港通及深港通持股紀錄](http://www.hkexnews.hk/mutualmarketsdw/main.htm)  
The code is CCASS code, you can reference [HKEX website](http://www.hkex.com.hk/mutual-market/stock-connect/eligible-stocks/view-all-eligible-securities?sc_lang=en) to to get stock code.

這是一個用Scrapy 的爬蟲, 從港交所拿每天滬港通及深港通的持股紀錄  
Code是CCASS 編號 不是股份編號，可在[港交所綱站](http://www.hkex.com.hk/mutual-market/stock-connect/eligible-stocks/view-all-eligible-securities?sc_lang=zh-hk)找到對應

##Demo 數據示範

http://www.zoeystudios.com/echarts.html 

You can enter 700 (e.g tencent stock code) 輸入700 (QQ 的股票號碼)

## Usage

After you download you can start use by following command
* scrapy crawl hkexnews (Get Today data)
* scrapy crawl hkexnews -o 123.json (will save the result to file 123.json in JSON format)
* scrapy crawl hkexnews -a date=20180921 (Get the data from Date 21-Sep-2018, the format is YYYYmmdd)

Due to limation from hkexnews, it only allow you download latest one year data. If you choose the day is not avaiable, the spider will handle as HTTP reponse 404. If the date is not trading day, also will reponse 404.

當你下載完之後就能用
因為港交所只可給你拿回一年內的數據，如果超出那日期，Spider 會自動當404 處理. 如果那天沒有交易，也會當404 處理.

## Change Log
* 2018-10-29
  * Remove selenium, direct use formrequest to improve crawl performance
  * change the input date format from yyyy-mm-dd to yyyymmdd.But will use yyyy-mm-dd format in DB
* 2018-10-28
  * Fix the code after hkexnews change the layout. 因為HKEX 在10月底改了板面
  * change the date format from yyyymmdd to yyyy-mm-dd. It is better to store in DB and query from Javascript


## Requirement 
* Scrapy
* <del>Selenium </del>
* <del>ChromeDriver</del> 

## Database (Optional)

Mongodb pipeline already implement you can uncomment below `#'hkexnews_scrapy.pipelines.MongoDBPipeline': 300,` in the `settings.py`  
You can apply mlab or create your own mongo db instance to use.

內置了 Mongodb pipeline模組，在`settings.py`裏配置 `'hkexnews_scrapy.pipelines.MongoDBPipeline': 300,`就可  
你可在MLAB 申請一個免費的 mongodb 或者自己建立.

## Setting
In the settings.py 

* MONGODB_URI # Mongodb URI
* MONGODB_DB  # Mongodb Name
* MONGODB_COLLECTION # Mongodb collection Name
* <del>CHROMEDRIVER_PATH # Chromedriver path</del>
* <del>CHROME_HEADLESS  # Chromedriver headless mode or not, default is headless mode</del>

## Todo

* No Idea now, please let me know if you want to enhance/ 暫時沒有想法，有意見請提出

## Remark
Old version was using selenium + chromedriver to pretend user to activtiy. If you would like to reference the code, you can go back to old version to check the code
