# ReadMe

## verify versions

```shell
java -version # see 21
native-image --version # see 21
```

## traditional build

```shell
mvn clean package && java -jar ./target/jibber-0.0.1-SNAPSHOT-exec.jar &
```

### test

```shell
curl http://localhost:8080/jibber
```

### kill process

```shell
fg # bring to foreground then Ctrl-C
```

### docker

1. build docker image
    ```shell
    docker build -f ./00-containerise/Dockerfile \
        --build-arg JAR_FILE=./target/jibber-0.0.1-SNAPSHOT-exec.jar \
        -t localhost/jibber:java.01 .
    ```
2. Query Docker to look at your newly built image:
    ```shell
    docker images | head -n2 && docker images localhost/jibber:java.01
    ```

3. Run this image as follows:
    ```shell
    docker run --rm -d --name "jibber-java" -p 8080:8080 localhost/jibber:java.01
    ```
   
4. Test
    ```shell
    curl http://localhost:8080/jibber
    ```
   
5. check log
    ```shell
    docker logs jibber-java
    ```
   
6. terminate container
    ```shell
    docker kill jibber-java
    ```

## build native image

### run `native` profile

```shell
mvn package -Pnative # take ~10min
```

### check and run

```shell
ls -lh target/jibber;
./target/jibber &
```

### docker the native image

1. build docker image
```shell
docker build -f ./01-native-image/Dockerfile \
    --build-arg APP_FILE=./target/jibber \
    -t localhost/jibber:native.01 .
```

2. Take a look at the newly built image:
```shell
docker images | head -n2 && docker images localhost/jibber:native.01
```

3. run docker image
```shell
docker run --rm -d --name "jibber-native" -p 8080:8080 localhost/jibber:native.01
```

4. test
```shell
curl http://localhost:8080/jibber && docker logs jibber-native
```

5. terminate the running docker
```shell
docker kill jibber-native
```


