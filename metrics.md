# Metrics

## access_log

**Logfile example**:    
5.101.0.209 - - [02/Feb/2020:04:22:32 -0500] "POST /vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php HTTP/1.1" 404 248 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"    
185.156.177.234 - - [02/Feb/2020:06:02:00 -0500] "\x03" 400 226 "-" "-"     
177.137.119.138 - - [02/Feb/2020:09:06:20 -0500] "-" 408 - "-" "-"        
177.137.119.138 - - [02/Feb/2020:09:11:40 -0500] "-" 408 - "-" "-"     
     
**Grok field names**:    
clientip, ident, auth, timestamp, verb, request, httpversion, rawrequest, response, bytes, referrer, agent       

**Metrics**:  

**1) access_log_counter**      
It is a counter metric for labels: verb, request, response. It shows the number of appearances for each combination of labels.     

**Metric example**:        
access_log_counter{code="200",method="OPTIONS",request="/"} 1       
access_log_counter{code="400",method="",request=""} 30        
access_log_counter{code="400",method="GET",request="/"} 25       
access_log_counter{code="400",method="GET",request="/w00tw00t.at.ISC.SANS.DFind:)"} 1       

**2) access_log_gauge**      
It is a gauge metric for label: request and value: response. It shows the last value of response for each request.      

**Metric example**:        
access_log_gauge{request=""} 400      
access_log_gauge{request="/"} 400       
access_log_gauge{request="/%73%65%65%79%6F%6E/%68%74%6D%6C%6F%66%66%69%63%65%73%65%72%76%6C%65%74"} 404       
access_log_gauge{request="/%75%73%65%72%2e%70%68%70"} 404        

**3) access_log_histogram**      
It is a histogram metric for label: request and value: response. It shows the number of appearances of each request in buckets: response<=200, response<=400, response<=403, response<=404, response<=408.        

**Metric example**:      
access_log_histogram_bucket{request="",le="200"} 0        
access_log_histogram_bucket{request="",le="400"} 30        
access_log_histogram_bucket{request="",le="403"} 30        
access_log_histogram_bucket{request="",le="404"} 30        
access_log_histogram_bucket{request="",le="408"} 49        
access_log_histogram_bucket{request="",le="+Inf"} 49        
access_log_histogram_sum{request=""} 19752        
access_log_histogram_count{request=""} 49        
access_log_histogram_bucket{request="/",le="200"} 1         
access_log_histogram_bucket{request="/",le="400"} 26        
access_log_histogram_bucket{request="/",le="403"} 173        
access_log_histogram_bucket{request="/",le="404"} 173        
access_log_histogram_bucket{request="/",le="408"} 173        
access_log_histogram_bucket{request="/",le="+Inf"} 173        
access_log_histogram_sum{request="/"} 69441        
access_log_histogram_count{request="/"} 173        

**3) access_log_summary**      
It is a histogram metric for label: request and value: response. It shows the number of appearances of each request in buckets: response<=200, response<=400, response<=403, response<=404, response<=408.        

**Metric example**:      
