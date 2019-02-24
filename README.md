# bloom rest api cache proxy


## how to running

```code
docker-compose up -d
```

## test result

* with bloom server

> note must with Bloom-Request-Shard header

```code

curl -X GET \
  http://localhost:8080/userinfo \
  -H 'Bloom-Request-Shard: 0' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: bc168c7c-3b8b-471d-aa01-6eb6cb0d421c' \
  -H 'cache-control: no-cache'


curl -X GET \
  http://localhost:8081/userinfo2 \
  -H 'Bloom-Request-Shard: 1' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: d13543ca-a031-47e3-b47a-996a6faaad53' \
  -H 'cache-control: no-cache'


```

* with openresty proxy

```code
http://localhost:9000/userinfo
http://localhost:9000/userinfo2
```

## how to validate if data is cached

* with log

```code
just see the log result with docker-compose logs -f
```

* with http request header

```code
curl -v http://localhost:9000/userinfo
```

result:

```code
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 9000 (#0)
> GET /userinfo HTTP/1.1
> Host: localhost:9000
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Server: openresty/1.13.6.2
< Date: Sun, 24 Feb 2019 01:53:39 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Connection: keep-alive
< Vary: ETag
< ETag: "8366b719422e8bc9"
< Bloom-Status: HIT
< 
{"age":333,"name":"dalongdempo"}
```