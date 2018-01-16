# nginx-online-stats
This patche adds a ```fullstat``` module which extend nginx (tested with nginx 1.2.1) statistics functionality by introducing the new internal page updated in realtime.

The main advantage of this software in comparison with lua or statd implementations is that it is very fast without noticiable affect on overall nginx performance.

Used in production for years, considered stable.

## Configuration file

To activate statistics for nginx, which is compiled with this patch you can simply create in any ```server {}``` block the following ```location```:

```
location /nginx-status {
    full_status on;
    #allow 127.0.0.1/24;
    deny  all;
}
```

After that you can access http://your_website.com/nginx-status to see the statistics. Allow directive allows to limit access to this page.

## Statistics page example

The page includes the table each row of which represents statistics of one virtualhost:

```
virthost                             requests     active_msec      traffic_in     traffic_out
example.com                                12            9933          556495          400007
example1.com                                1             132             173            3020
example2.com                             1313          353251          866525       239429133
example3.com                                5               9            1499            9920
example4.com                               38            1093           17837          810103
example5.com                                3           17973            1084           23572
example6.com                              119            4292           54530          766747
_NGINX_TOTAL_:                           1491          386683         1498143       241442502

```
