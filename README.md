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
