# Quals Challenge: Something's Out There #

**Category:** Communication System
**Relative Difficulty:** 5/5
**Author:** [Red Balloon Security](https://www.redballoonsecurity.com/)

Now let's combine everything you've learned for a real tough one!


## Building ##

This repository contains two Docker images: The `generator` and `solver`.
You can build them both with:

```sh
make build
```

The resulting Docker images will be tagged as `nena:generator`
and `nena:solver`.

You can also build just one of them with `make generator` or `make solver`
respectively.

Building the `generator` container requires having already built the
`generator-base` container (see the `generator-base` folder).


## Deploying ##

This challenge has nothing to deploy. It's self-contained within the files
generated by the `generator`. See the top-level `README.md` for more
information on using the `generator` container.


## Testing ##

See top-level `README.md` file for more information on using the `solver`
container.


## Notes ##

The contestants are given a .wav file and an AES 256 key.

* In the same fashion as Major Tom, they will find that it is QPSK and
  demodulate it.
* This time however there is some added noise and channel emulation as
  well as a fake flag encoded into the noise made to look like motor cross
  talk.
* After decoding the QPSK signal, they will have to convert it to binary,
  the same way as Major Tom.
* From here, if demodulated correctly they will see the song lyrics with
  a block of encrypted data in between all encapsulated in CCSDS Telemetry
  packets.
* They carve out the data and try to decrypt with the provided key, however
  I they don’t implement the Reed-Solomon ECC portion of the CCSDS standard
  it will not decrypt.
* Decrypt the message to see a set of TLE messages, the names are recognizable
  as the same song lyrics mostly, but out of order.
* Re ordering the TLE messages based on the International designator will give
  you the correct flag.