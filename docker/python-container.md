# python-container



```
docker run                              \
        --net docker-net1                                       \
        --ip 172.17.8.19                                        \
        -d                                                      \
        -p 0.0.0.0:8000:8000                                    \
        --name py36port81                                       \
        --mount type=bind,src="/root/docker-op/python36/src1",dst="/root/py36/src1"  \
        python:3.6
```

