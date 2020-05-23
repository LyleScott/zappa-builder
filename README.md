# zappa-builder

Build a Zappa app within a docker container that mimicks the lambda env.

> The work here is for a Django app, so edit to taste.

## Usage

Check out as a submodule in the root of your project:

```bash
git submodule add https://github.com/LyleScott/zappa-builder zappa_build
```

Build the app:

```bash
docker build -t zappabuild -f zappa_build/Dockerfile .
```

You have a few options for telling the container about your AWS credentials that boto needs:

Mount your AWS credentials and config files:

```bash
docker run -it -v ~/.aws:/root/.aws zappabuild dev
```

If you needed to specify a profile to use from `/root/.aws/credentials`:

```bash
docker run -it \
  -v ~/.aws:/root/.aws \
  -e AWS_PROFILE=prod \
  zappabuild dev
```

If you needed to use environment variables:

> These are likely defined in your `~/.aws/credentials` file

```bash
docker run -it \
  -e AWS_ACCESS_KEY_ID=foobar \
  -e AWS_SECRET_ACCESS_KEY=foobar \
  -e AWS_DEFAULT_REGION=us-east-1 \
  zappabuild dev
```
