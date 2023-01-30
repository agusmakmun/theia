First time to install the `package.json`

```
yarn install
```


Building the image:

```
docker build -t secure-box-image -f Dockerfile .
```

Running the container:

```
docker run --user root -p 80:3000 -v "/home:/home/project:cached" --name secure-box-container -it secure-box-image
```
