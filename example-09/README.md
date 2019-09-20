# Pushing Images

Satisfied with our latest image, we can push it to a registry. Docker Hub is a
convenient public registry to work with. Go to dockerhub.com and log in if you
are an existing user, or create a new account.

Re-tag the latest image we created:

```console
$ docker tag go-hello-world:v5 <docker hub username>/go-hello-world:v6
```

And push it:

```console
$ docker push <docker hub username>/go-hello-world:v6
```

Anyone else can now pull and run your image!
