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
access_log_counter{code="400",method="POST",request="/HNAP1/"} 1       
