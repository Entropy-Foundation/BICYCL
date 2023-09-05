BICYCL
======

BICYCL is an Open Source C++ library that implements arithmetic in the ideal
class groups of imaginary quadratic fields, together with a set of cryptographic
primitives based on class groups. We modify the implementation to be used for our Class-Group DKG at: https://github.com/Entropy-Foundation/class-group. In particular we add pippenger's multi-exponentiation algorithm for class group elements, multi-encryption, conversion between GMP's Mpz and Miracl's BIG type, and some other minor changes.

How to build the library:

Step 1:
Build the Miracl core library at (https://github.com/miracl/core/tree/master/cpp). Move all files in the cpp directory to a new directory "miracl" and run ``python3 config32.py''. Select BLS 12-381 curve. Build the curve and copy the miracl folder to /usr/local/include, rename core.a to libcore.a and copy libcore.a file to /usr/local/lib. 

Step 2:
Follow the instructions here (https://crypto.lirmm.net/bicycl/install.html) to build and install this library.
