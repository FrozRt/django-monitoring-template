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
5) Do not forget replace target containers naming in prometheus.yml
6) Add prometheus lib using your package manager:  
`pip install django-prometheus`  
7) Next you should correctly configure your prometheus for metrics collecting in django project:
* settings.py  
```
INSTALLED_APPS=[
    ...........
    'django_prometheus',]

MIDDLEWARE:[
    'django_prometheus.middleware.PrometheusBeforeMiddleware',
    ......
    'django_prometheus.middleware.PrometheusAfterMiddleware']
```
and replace your regular db backend on:
```
'ENGINE': 'django_prometheus.db.backends.your_rdbbms',
```

* urls.py  
```
url('', include('django_prometheus.urls')),
```
  
You can get acquainted with more exporters on  [prometheus](https://prometheus.io/docs/instrumenting/exporters/) official website.  
My advice for node exporter dashboard - 11074  
Base dashboard for nginx metrics - 5063
