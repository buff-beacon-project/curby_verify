# CURBy Verifier and DIRNG analysis

This repository holds the software used to verify randomness from [CURBy](https://random.colorado.edu) according to the Device-independent
randomness generation protocol.

To perform a verification of a given CURBy-Q round, you will first need [docker and docker-compose](https://www.docker.com/) installed. (You can also use other container managers like [podman](https://podman.io/)).

## Verification

First download the [docker-compose.yaml](./docker-compose.yaml) file.

```sh
wget https://raw.githubusercontent.com/buff-beacon-project/curby_verify/refs/heads/main/docker-compose.yaml
```

To run the verification of a specific round (for example round 123), run
a command like this:

```sh
docker compose run --rm verify 123
```

This will temporarily boot up the [extractor server](https://github.com/buff-beacon-project/trevisan_python_interface),
and use the [CURBy JS Library](https://github.com/buff-beacon-project/curby-js-client)
to fetch and verify the necessary data. Then it will run the raw data
through the extractor and ensure the output matches what was reported.

The [index.ts](./index.ts) file also serves as a demonstration of
how to use the CURBy Library to fetch randomness data.

## Development

First clone this repository:

```sh
git clone https://github.com/buff-beacon-project/curby_verify.git
```

Change the docker-compose.yaml

Then build, using docker compose:

```sh
docker compose -f docker-compose.local.yaml build
docker compose -f docker-compose.local.yaml run verify 123
```
