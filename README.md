# Shell-script

## 什麼是shell script?

shell script又稱程式化腳本，shell是一個文字介面底下讓我們與系統溝通的一個工具介面；script則是腳本的意思，所以shell script就是一個針對shell
所寫的劇本。

## 如何使用shell

建立一個shell的檔案(.sh)，並修改內容
```
vi shell.sh
```

shell.sh 檔案必須要具備可讀與可執行 (rx) 的權限

* 絕對路徑：使用 
```
/home/dmtsai/shell.sh
```

* 相對路徑：假設工作目錄在 /home/dmtsai/ ，則使用
```
./shell.sh
```

* 以 bash 程式來執行：
```
bash shell.sh
```
或是
```
sh shell.sh
```

## 撰寫shell的好習慣

建議要養成良好的 script 撰寫習慣，在每個 script 的檔頭(檔案最上方)處記錄好：
* script 的功能；
* script 的版本資訊；
* script 的作者與聯絡方式；
* script 的版權宣告方式；
* script 的 History (歷史紀錄)；
* script 內較特殊的指令，使用『絕對路徑』的方式來下達；
* script 運作時需要的環境變數預先宣告與設定。


```
#!/bin/bash
# Program:
#	User inputs his first name and last name.  Program shows his full name.
# History:
# 2015/07/16	VBird	First release
```

## 讀入使用者所輸入的字串

使用read -p "你想問使用者的話" 使用者輸入的字串存成的變數名稱
輸出使用echo，$name為上方接收到使用者所輸入的字串
```
read -p "what you name " name
echo "my name is " $name
```

## 將字串寫入檔案

可以將字串寫入文件內，每次寫入會清除前一次的檔案。換行可以直接換行或是輸入/n

```
echo "what do you want to insert" > abc.txt;
```

## 自動部屬vhost的config檔案範例

COLOR_REST和COLOR_RED為改變字串顏色之變數。
echo -e是為了顯示ASCII code的顏色編碼，不加上-e無法正確地顯示

```
#Program:
#	user enter website's URL & DocumentName , Program create new file and insert the vhost config
#History:
#	2019/09/11  -  first time commit 


COLOR_REST='\e[0m';
COLOR_RED='\e[1;31m';

read -p "please enter your webiste $(echo -e $COLOR_RED"URL"$COLOR_REST) " url

read -p "please enter your website $(echo -e $COLOR_RED"DocumentName"$COLOR_REST) " document

touch /etc/httpd/conf.d/$document.conf;

echo "enter your config file ...";

echo -e '<VirtualHost *:80>
    ServerName '$url'
    DocumentRoot  /var/www/html/'$document'
    ErrorLog logs/'$document'
    CustomLog logs/'$document'_log common

    <Directory "/var/www/html/'$document'">
        Options FollowSymLinks
        AllowOverride None
        Order allow,deny
        allow from all
    </Directory>
</VirtualHost>' > /etc/httpd/conf.d/$document.conf;

echo "vhost auto deploy is successful";
```
