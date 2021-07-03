### Django project monitoring template  
Deploy your monitoring step by step:
1) Easify your deploy using any ci/cd system created by Bitbucket, Gitlab or Github
2) Potentially you need to update your docker-compose for using all features
3) Add nginx metrics location to your nginx config:  
```
location /nginx_metrics {   
    stub_status on;  
    access_log off;  
}
```
4) This monitoring template use project docker network and that means you should connect to external project network in the same server 

You can get acquainted with more exporters on  [prometheus](https://prometheus.io/docs/instrumenting/exporters/) official website.  
My advice for node exporter dashboard - 11074  
Base dashboard for nginx metrics - 5063
