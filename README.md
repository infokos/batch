# bitcoin in tiny pieces

These are Python scripts made from scracth to play with Bitcoin addresses: public, private, WIF...

The scripts are compatible with Python 2 and Python 3.

## before start

Install base58 for Python (tested with base58-1.0.0):

	$ pip install base58

## examples of use

	$ ./bitcoin-public-from-private.py 0x01
		79be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798 483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8

	# with VERBBOSE = True in bitcoin-address-from-public-key.py :
	$ ./bitcoin-public-from-private.py 0x01 | ./bitcoin-address-from-public-key.py
		pubkey = 0479be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798483ada7726a3c4655da4fbfc0e1108a8fd17b448a68554199c47d08ffb10d4b8

		Uncompressed public key:
		key_hash =      91b24bf9f5288532960ac687abb035127b1d28a5
		checksum =      0074ffe0526d823be09b39865422a1d6135afc85afb0a6863c58e9fe89989170
		key_hash + checksum =   0091b24bf9f5288532960ac687abb035127b1d28a5 0074ffe0
		bitcoin address =       1EHNa6Q4Jz2uvNExL497mE43ikXhwF6kZm

		Compressed public key:
		key_hash =      751e76e8199196d454941c45d1b3a323f1433bd6
		checksum =      510d1634d943109b69da527ef5948106f22b655fb5193b4e9ef7e4dcd342d245
		key_hash + checksum =   00751e76e8199196d454941c45d1b3a323f1433bd6 510d1634
		bitcoin address =       1BgGZ9tcN4rm9KBzDn7KprQz87SZ26SAMH

		Hybrid public key:
		key_hash =      7083929bc41c16f2337fbcd10cd73df8a4e2a2bb
		checksum =      74a0a7a97d3c7f60adceb3475880abac2231bc02b4f91753ae6dc20fcabe96ae
		key_hash + checksum =   007083929bc41c16f2337fbcd10cd73df8a4e2a2bb 74a0a7a9
		bitcoin address =       1BFvJKK757eGXdNHkXkgem4fWZU28d1cnk

	$ ./bitcoin-wif-from-private-key.py 0x01
		privkey = 8001

		For compressed public key:
		checksum =      553bc06a6f4e0f4d575a9b43e2eb82546131dccec1c3a99151ee08cb5972c8a9
		key + checksum =        800101 553bc06a
		bitcoin address =       5rM1SJieKB

		For uncompressed public key:
		checksum =      e27a1d3a74fa86f9a913e996663ea76fc2333c3b77ae33ff18349a549fd36721
		key + checksum =        8001 e27a1d3a
		bitcoin address =       26k9aD1PF

	$ echo 0x01 | ./bitcoin-public-from-private.py | ./bitcoin-address-from-public-key.py | xargs -I {} ./bitcoin-get-address-balance.py {}

		address         = 1EHNa6Q4Jz2uvNExL497mE43ikXhwF6kZm
		total_received  = 4.87126141 Bitcoin
		final_balance   = 0 Bitcoin


		address         = 1BgGZ9tcN4rm9KBzDn7KprQz87SZ26SAMH
		total_received  = 0.14609494 Bitcoin
		final_balance   = 0 Bitcoin


		address         = 1BFvJKK757eGXdNHkXkgem4fWZU28d1cnk
		total_received  = 0 Bitcoin
		final_balance   = 0 Bitcoin

	# Use a SHA256 hashed string as private key, and check if it has been used:
	$ ./bitcoin-test-address-balance.sh satoshi
		satoshi
		address         = 1ADJqstUMBB5zFquWg19UqZ7Zc6ePCpzLE
		total_received  = 0.00375370 Bitcoin
		final_balance   = 0 Bitcoin


		address         = 1xm4vFerV3pSgvBFkyzLgT1Ew3HQYrS1V
		total_received  = 0.00111100 Bitcoin
		final_balance   = 0 Bitcoin


		address         = 16uTbx4gagzvEzyeSh57SdxZNbZnTrRoks
		total_received  = 0 Bitcoin
		final_balance   = 0 Bitcoin

## notes of usage

The scripts contain useful comments and links to documentation. Also contain configuration variables that can be preset:

Each script can be configured with at least the variable `VERBOSE` which can be `True` or `False`: if you want to concatenate scripts in command-line with `|`, you need to set `VERBOSE = False`.

`bitcoin-address-from-public-key.py` contains the variable `COMPRESS_PUBKEY` that accepts the values 0 to 3 in order to print uncompressed, compressed, hybrid, or all of the valid formats of a public bitcoin address.

`bitcoin-wif-from-private-key.py` contains the variable `COMPRESS_PUBKEY` that accepts the values 0 to 2 in order to print uncompressed, compressed, or both formats of WIF.

## notes for Windows users

The folder `batchs for Windows` contains `.bat` files for ease of usage with Windows:

* be sure you have Python in your `%PATH%`, or prepend the Python path to `python` inside each `.bat`

* modify inside each `.bat` the complete path to the folder where you've copied all these Python scripts

* Now usage in Windows is as easy as with Linux:

        C:\> echo 0x01 | bitcoin-public-from-private | bitcoin-address-from-public-key
	        1EHNa6Q4Jz2uvNExL497mE43ikXhwF6kZm
	        1BgGZ9tcN4rm9KBzDn7KprQz87SZ26SAMH
	        1BFvJKK757eGXdNHkXkgem4fWZU28d1cnk

Please, see `notes of usage` above for configuring outputs and using with `|` concatenation.

## License

Release under [GPL 3](https://www.gnu.org/licenses/gpl-3.0.en.html).