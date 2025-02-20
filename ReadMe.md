# Example of signing a firmware artifact for a RP2350 Pico2
## PRE-ALPHA - NOT READY FOR USE BY OTHERS

This example uses our marketplace action 
[rp2350-firmware-signer](https://github.com/marketplace/actions/rp2350-firmware-signer)
to sign the firmware with our pre-bundled tool chain. This
version is for the RP2350 (pico2) but we can support many chipsets.

* [do-sign.yml](.github/workflows/do-sign.yml)
  Most of the work for for calling the pre-build signing 
  tool chain is in this file.  To make it work you submit a
  commit to the repo which will trigger the do-sign.yml action
  to run. It will call our pre-packaged firmware signer which 
  uses our pre-packaged docker images to do the signing and 
  then saves the output as a signed artifact.    

* [unsigned/blink_fast.uf2](unsigned/blink_fast.uf2)
  is a pre-compiled binary for the pico2 built from 
  [rp2350-ex-blink-fast](https://github.com/immutaverse/rp2350-ex-blink-fast).  It is an example of a unsigned binary.  
  We included it here in binary form for simplicity 
  We would normally build from source then sign.  You can clone
  the sample repo and build the binary yourself if you have 
  the arm compilers and tool chain installed.  You can also 
  use our pre-built tool-chains that can build it from inside your
  CICD using a git action. 

* [signed](signed) directory to store our signed artifact
  once we get it signed.  we will add a timestamp to each
  when copying to this directory to make it easier to 
  see the output from multiple signing events. 



## Important: 
* NOTE: We pull the signing secret from a variable defined for our 
  repository.  When you fork this so you can sign your own key
  you will need to declare your own secret with a private signing 
  key. 

* We normally avoid checking binaries into github source repositories.
  it is better to save them in a binary repository or a repo 
  dedicated to storing binary releases.  We only do it here in
  this repo to keep the sample as small and self contained 
  as possible.  If you need binary components as part of a build
  that are pre-built in other CICD then store them in other repo
  and use the github submodule feature to make them availabile
  for the current build.




