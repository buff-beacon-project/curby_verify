# CURBy Verifier and DIRNG analysis and Trevisan extractor server

This repository holds the software used by [CURBy](https://random.colorado.edu)
to analyze data from the NIST looophole-free Bell experiment and to extract randomness
according to the Device-independent randomness generation protocol.

It also contains another docker image to perform a verification of a specified round
of randomness from CURBy-Q.

## Verifier

To perform a verification of a given CURBy-Q round, you will first need [docker and docker-compose](https://www.docker.com/) installed. (You can also use other container managers like [podman](https://podman.io/)).

### Setup

First clone this repository:

```sh
git clone https://github.com/buff-beacon-project/trevisan_python_interface
cd trevisan_python_interface
```

Then build, using docker compose:

```sh
docker compose --profile=verify build
```

### Verification

To run the verification of a specific round (for example round 123), run
a command like this:

```sh
docker compose --profile verify run --rm verify 123
```

This will temporarily boot up the extractor server (described below),
and use the [CURBy JS Library](https://github.com/buff-beacon-project/curby-js-client)
to fetch and verify the necessary data. Then it will run the raw data
through the extractor and ensure the output matches what was reported.

The [index.ts](./verifier/index.ts) file also serves as a demonstration of
how to use the CURBy Library to fetch randomness data.