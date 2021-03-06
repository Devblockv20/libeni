=======================
Simulate ENI Operations
=======================

We provide two CLI tools `eni_gas` and `eni_run`, which simulate how the ENI
operations are called in a shared library from EVM.

Check the usage of the tools by running it without any arguments.

.. code::

  NAME
    eni_gas - the estimated gas cost when running the ENI operation
    eni_run - run the ENI operation and print the result in JSON format

  SYNOPSIS
    eni_gas <LIBPATH> <OP> <JSON>
    eni_run <LIBPATH> <OP> <JSON>

  DESCRIPTION
    LIBPATH - path to the shared library
    OP      - name of the ENI operation
    JSON    - parameters passed to the operation in JSON format

Test Prebuilt Shared Libraries
------------------------------

Here we demonstrate how to test the ENI operation built from our examples
and tools with the CLI tools `eni_gas` and `eni_run`.

Test "eni_reverse.so" (`examples/eni/reverse`)
``````````````````````````````````````````````

.. code:: bash

  eni_gas ${LIBENI_PATH}/lib/eni_reverse.so reverse '["Hello World!"]'
  eni_run ${LIBENI_PATH}/lib/eni_reverse.so reverse '["Hello World!"]'

The first call `eni_gas` will output `12`, and
the second one `eni_run` will output `["!dlroW olleH"]`.

Test "eni_crypto.so" (`tools/eni_crypto`)
`````````````````````````````````````````

Get the JSON files for testing from the directory `test/t0004 <test/t0004>`_.

.. code:: bash

  eni_gas ${LIBENI_PATH}/lib/eni_crypto.so rsa_encrypt $(cat pub_encrypt.json)
  eni_run ${LIBENI_PATH}/lib/eni_crypto.so rsa_encrypt $(cat pub_encrypt.json)
  eni_gas ${LIBENI_PATH}/lib/eni_crypto.so rsa_decrypt $(cat priv_decrypt.json)
  eni_run ${LIBENI_PATH}/lib/eni_crypto.so rsa_decrypt $(cat priv_decrypt.json)

Output for the above lines.

.. code:: bash

  12
  ["An encrypted hex-string that is 512 characters in length."]
  256
  ["Hello World!"]
