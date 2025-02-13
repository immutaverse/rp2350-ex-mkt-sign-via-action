# Example of signing a firmware artifact for a RP2350 Pico2
This example uses our marketplace action to sign firmware 
for a RP2350 that has been configured for secure boot.

* [.github/workflows/dosign.yml](.github/workflows/dosign.yml)
  Most of the work for this is in .  The way this works is that
  you you submit a commit to the repo which will trigger the 
  do-sign.yml action to run. It will call our pre-packaged 
  firmware signer which uses our pre-packaged docker images 
  to do the signing and then saves the output as a signed 
  artifact.    
  
* [unsigned/blink_fast.uf2](unsigned/blink_fast.uf2)
  a pre-compiled binary for the pico2 built from 
  https://github.com/immutaverse/rp2350-ex-blink-fast 
  as an example of a unsigned binary.   Included here 
  in binary form for simplicity in this example.  We would
  normally build from source then sign.


To make it obvious action will copy the output to ./signed directory
out in this repository and commit and push that change so it is 
available the next time you do a git pull. 

NOTE: We pull the signing secret from a variable defined for our 
repository.  When you fork this so you can sign your own file.
you will need to declare your own secret with a private signing 
key. 



uses: actions/rp2350-firmware-signer@v2
  with:
    # Path to the artifact serving as the subject of the attestation. Must
    # specify exactly one of "subject-path", "subject-digest", or
    # "subject-checksums". May contain a glob pattern or list of paths
    # (total subject count cannot exceed 1024).
    subject-path:

    # SHA256 digest of the subject for the attestation. Must be in the form
    # "sha256:hex_digest" (e.g. "sha256:abc123..."). Must specify exactly one
    # of "subject-path", "subject-digest", or "subject-checksums".
    subject-digest:

    # Subject name as it should appear in the attestation. Required when
    # identifying the subject with the "subject-digest" input.
    subject-name: