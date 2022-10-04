
```
thor@jump_host ~$ cat /opt/news.txt 
5ecur3
```


```
thor@jump_host ~$ kubectl create secret generic news --from-file=/opt/news.txt 
secret/news created
```

