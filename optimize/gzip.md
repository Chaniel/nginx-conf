```bash
server {

# gzip config
  gzip on;
  gzip_min_length 100;
  gzip_comp_level 3;
  
  gzip_types text/plain;
  gzip_types text/css;
  gzip_types text/javascript;
  
  gzip_disable "msie6";
  
}

```

gzip test, compare the size using gzip and not using gzip.
```bash
# curl -H 'Accept-Encoding:gzip,deflate' http://ip/css/style.css > style_compressed.css
# curl http://ip/css/style.css > style_uncompressed.css
# ls -lh
```
