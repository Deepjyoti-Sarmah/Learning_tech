- #### Solana Overview[](https://solang.readthedocs.io/en/latest/targets/solana.html#solana-overview "Permalink to this heading")
		- As the underlying Solana environment is different than that of Ethereum, Solidity inner workings have been modified to function properly. For example, A Solidity contract on Solana utilizes two accounts: a data account and a program account. The program account stores the contract’s executable binary and owns the data account, which holds all the storage variables. On Ethereum a single account can store executable code and data.
- #### Compute budget
		- On Ethereum, when calling a smart contract function, one needs to specify the amount of gas the operation is allowed to use. Gas serves to pay for a contract execution on chain and can be a way for giving a contract priority execution when extra gas is offered in a transaction. Each EVM instruction has an associated gas value, which translates to real ETH cost. Provided that one can afford all the gas expenses, there is no upper boundary for the amount of gas limit one can provide in a transaction, so Solidity for Ethereum has gas builtins, like `gasleft`, `block.gaslimit`, `tx.gasprice` or the Yul `gas()` builtin, which returns the amount of gas left for execution.
		- On the other hand, Solana is optimized for low latency and high transaction throughput and has an equivalent concept to gas: compute unit. Every smart contract function is allowed the same quantity of compute units (currently that value is 200k), and every instruction of a contract consumes exactly one compute unit. There is no need to provide an amount of compute units for a transaction and they are not charged, except when one wants priority execution on chain, in which case one would pay per compute unit consumed. Therefore, functions for gas are not available on Solidity for Solana.
- ## Using the Anchor client library[](https://solang.readthedocs.io/en/latest/targets/solana.html#using-the-anchor-client-library "Permalink to this heading")
		
		Some notes on using the anchor javascript npm library.
		
		-   Solidity function names are converted to camelCase. This means that if in Solidity a function is called `foo_bar()`, you must write `fooBar()` in your javascript.
		    
		-   Anchor only allows you to call `.view()` on Solidity functions which are declared `view` or `pure`.
		    
		-   Named return values in Solidity are also converted to camelCase. Unnamed returned are given the name `return0`, `return1`, etc, depending on the position in the returns values.
		    
		-   Only return values from `view` and `pure` functions can be decoded. Return values from other functions and are not accessible. This is a limitation in the Anchor library. Possibly this can be fixed.
		    
		-   In the case of an error, no return data is decoded. This means that the reason provided in `revert('reason');` is not available as a return value.
		    
		-   Number arguments for functions are expressed as `BN` values and not plain javascript `Number` or `BigInt`.
		    
		
		## Calling Anchor Programs from Solidity[](https://solang.readthedocs.io/en/latest/targets/solana.html#calling-anchor-programs-from-solidity "Permalink to this heading")
		
		It is possible to call [Anchor Programs](https://github.com/coral-xyz/anchor) from Solidity. You first have to generate a Solidity interface file from the IDL file using the [Generate Solidity interface from IDL](https://solang.readthedocs.io/en/latest/running.html#idl-command). Then, import the Solidity file in your Solidity using the `import "...";` syntax. Say you have an anchor program called `bobcat` with a function `pounce`, you can call it like so:
		
		import "bobcat.sol";
		import "solana";
		
		contract example {
		    function test(address a, address b) public {
		        // The list of accounts to pass into the Anchor program must be passed
		        // as an array of AccountMeta with the correct writable/signer flags set
		        AccountMeta[2] am = [
		            AccountMeta({pubkey: a, is_writable: true, is_signer: false}),
		            AccountMeta({pubkey: b, is_writable: false, is_signer: false})
		        ];
		
		        // Any return values are decoded automatically
		        int64 res = bobcat.pounce{accounts: am}();
		    }
		}
		
		## Setting the program_id for a contract[](https://solang.readthedocs.io/en/latest/targets/solana.html#setting-the-program-id-for-a-contract "Permalink to this heading")
		
		When developing contracts for Solana, programs are usually deployed to a well known account. The account can be specified in the source code using an annotation `@program_id`. If you want to instantiate a contract using the `new ContractName()` syntax, then the contract must have a program_id annotation.
		
		@program_id("Foo5mMfYo5RhRcWa4NZ2bwFn4Kdhe8rNK5jchxsKrivA")
		contract Foo {
		    function say_hello() public pure {
		        print("Hello from foo");
		    }
		}
		
		contract Bar {
		    Foo public foo;
		
		    function create_foo(address new_address) public {
		        foo = new Foo{address: new_address}();
		    }
		
		    function call_foo() public pure {
		        foo.say_hello();
		    }
		}
		
		Note
		
		The program_id `Foo5mMfYo5RhRcWa4NZ2bwFn4Kdhe8rNK5jchxsKrivA` was generated using the command line:
		
		solana-keygen grind --starts-with Foo:1
		
		## Setting the payer, seeds, bump, and space for a contract[](https://solang.readthedocs.io/en/latest/targets/solana.html#setting-the-payer-seeds-bump-and-space-for-a-contract "Permalink to this heading")
		
		When a contract is instantiated, there are two accounts required: the program account to hold the executable code and the data account to save the state variables of the contract. The program account is deployed once and can be reused for updating the contract. When each Solidity contract is instantiated (also known as deployed), the data account has to be created. This can be done by the client-side code, and then the created blank account is passed to the transaction that runs the constructor code.
		
		Alternatively, the data account can be created by the constructor, on chain. When this method is used, some parameters must be specified for the account using annotations. Those are placed before the constructor. If there is no constructor present, then an empty constructor can be added. The constructor arguments can be used in the annotations.
		
		@program_id("Foo5mMfYo5RhRcWa4NZ2bwFn4Kdhe8rNK5jchxsKrivA")
		contract Foo {
		
		    @space(500 + 12)
		    @seed("Foo")
		    @seed(seed_val)
		    @bump(bump_val)
		    @payer(payer)
		    constructor(address payer, bytes seed_val, bytes1 bump_val) {
		        // ...
		    }
		}
		
		Creating an account needs a payer, so at a minimum the `@payer` annotation must be specified. If it is missing, then the data account must be created client-side. The `@payer` requires an address. This can be a constructor argument or an address literal.
		
		The size of the data account can be specified with `@space`. This is a `uint64` expression which can either be a constant or use one of the constructor arguments. The `@space` should at least be the size given when you run `solang -v`:
		
		$ solang compile --target solana -v examples/solana/flipper.sol
		...
		info: contract flipper uses at least 17 bytes account data
		...
		
		If the data account is going to be a [program derived address](https://docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses), then the seeds and bump have to be provided. There can be multiple seeds, and an optional single bump. If the bump is not provided, then the seeds must not create an account that falls on the curve. The `@seed` can be a string literal, or a hex string with the format `hex"4142"`, or a constructor argument of type `bytes`. The `@bump` must a single byte of type `bytes1`.
		
		## Transferring native value with a function call[](https://solang.readthedocs.io/en/latest/targets/solana.html#transferring-native-value-with-a-function-call "Permalink to this heading")
		
		The Solidity language on Ethereum allows value transfers with an external call or constructor, using the `auction.bid{value: 501}()` syntax. Solana Cross Program Invocation (CPI) does not support this, which means that:
				- Specifying `value:` on an external call or constructor is not permitted
				- The `payable` keyword has no effect
				-  `msg.value` is not supported

	- Note
		
		A naive way to implement this is to let the caller transfer native balance and then inform the callee about the amount transferred by specifying this in the instruction data. However, it would be trivial to forge such an operation.
		
		## Receive function[](https://solang.readthedocs.io/en/latest/targets/solana.html#receive-function "Permalink to this heading")
		
		In Solidity the `receive()` function, when defined, is called whenever the native balance for an account gets credited, for example through a contract calling `account.transfer(value);`. On Solana, there is no method that implements this. The balance of an account can be credited without any code being executed.
		
		`receive()` functions are not permitted on the Solana target.
		
		## `msg.sender` not available on Solana[](https://solang.readthedocs.io/en/latest/targets/solana.html#msg-sender-not-available-on-solana "Permalink to this heading")
		
		On Ethereum, `msg.sender` is used to identify either the account that submitted the transaction, or the caller when one contract calls another. On Ethereum, each contract execution can only use a single account, which provides the code and data. On Solana, each contract execution uses many accounts. Consider a rust contract which calls a Solidity contract: the rust contract can access a few data accounts, and which of those would be considered the caller? So in many cases there is not a single account which can be identified as a caller. In addition to that, the Solana VM has no mechanism for fetching the caller accounts. This means there is no way to implement `msg.sender`.
		
		The way to implement this on Solana is to have an authority account for the contract that must be a signer for the transaction (note that on Solana there can be many signers too). This is a common construct on Solana contracts.
		
				import 'solana';
				
				contract AuthorityExample {
				    address authority;
				    uint64 counter;
				
				    modifier needs_authority() {
				        for (uint64 i = 0; i < tx.accounts.length; i++) {
				            AccountInfo ai = tx.accounts[i];
				
				            if (ai.key == authority && ai.is_signer) {
				                _;
				                return;
				            }
				        }
				
				        print("not signed by authority");
				        revert();
				    }
				
				    constructor(address initial_authority) {
				        authority = initial_authority;
				    }
				
				    function set_new_authority(address new_authority) needs_authority public {
				        authority = new_authority;
				    }
				
				    function inc() needs_authority public {
				        counter += 1;
				    }
				
				    function get() public view returns (uint64) {
				        return counter;
				    }
				}
		
		
		## Builtin Imports[](https://solang.readthedocs.io/en/latest/targets/solana.html#builtin-imports "Permalink to this heading")
		
		Some builtin functionality is only available after importing. The following structs can be imported via the special builtin import file `solana`.
		
		import {AccountMeta, AccountInfo} from 'solana';
		
		Note that `{AccountMeta, AccountInfo}` can be omitted, renamed or imported via import object.
		
		// Now AccountMeta will be known as AM
		import {AccountMeta as AM} from 'solana';
		
		// Now AccountMeta will be available as solana.AccountMeta
		import 'solana' as solana;
		
		Note
		
		The import file `solana` is only available when compiling for the Solana target.
		
		### Builtin AccountInfo[](https://solang.readthedocs.io/en/latest/targets/solana.html#builtin-accountinfo "Permalink to this heading")
		
		The account info of all the accounts passed into the transaction. `AccountInfo` is a builtin structure with the following fields:
		
		address `key`
		
		The address (or public key) of the account
		
		uint64 `lamports`
		
		The lamports of the accounts. This field can be modified, however the lamports need to be balanced for all accounts by the end of the transaction.
		
		bytes `` data` ``
		
		The account data. This field can be modified, but use with caution.
		
		address `owner`
		
		The program that owns this account
		
		uint64 `rent_epoch`
		
		The next epoch when rent is due.
		
		bool `is_signer`
		
		Did this account sign the transaction
		
		bool `is_writable`
		
		Is this account writable in this transaction
		
		bool `executable`
		
		Is this account a program
		
		### Builtin AccountMeta[](https://solang.readthedocs.io/en/latest/targets/solana.html#builtin-accountmeta "Permalink to this heading")
		
		When doing an external call (aka CPI), `AccountMeta` specifies which accounts should be passed to the callee.
		
		address `pubkey`
		
		The address (or public key) of the account
		
		bool `is_writable`
		
		Can the callee write to this account
		
		bool `is_signer`
		
		Can the callee assume this account signed the transaction
		
		### Builtin create_program_address[](https://solang.readthedocs.io/en/latest/targets/solana.html#builtin-create-program-address "Permalink to this heading")
		
		This function returns the program derived address for a program address and the provided seeds. See the Solana documentation on [program derived addresses](https://edge.docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses).
		
		import {create_program_address} from 'solana';
		
		contract pda {
		    address token = address"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA";
		
		    function create_pda(bytes seed2) public returns (address) {
		        return create_program_address(["kabang", seed2], token);
		    }
		}
		
		### Builtin try_find_program_address[](https://solang.readthedocs.io/en/latest/targets/solana.html#builtin-try-find-program-address "Permalink to this heading")
		
		This function returns the program derived address for a program address and the provided seeds, along with a seed bump. See the Solana documentation on [program derived addresses](https://edge.docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses).
		
		import {try_find_program_address} from 'solana';
		
		contract pda {
		    address token = address"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA";
		
		    function create_pda(bytes seed2) public returns (address, bytes1) {
		        return try_find_program_address(["kabang", seed2], token);
		    }
		}
		
		## Solana Library[](https://solang.readthedocs.io/en/latest/targets/solana.html#solana-library "Permalink to this heading")
		
		In Solang’s Github repository, there is a directory called `solana-library`. It contains libraries for Solidity contracts to interact with Solana specific instructions. We provide two libraries: one for SPL tokens and another for Solana’s system instructions. In order to use those functionalities, copy the correspondent library file to your project and import it.
		
		### SPL-token[](https://solang.readthedocs.io/en/latest/targets/solana.html#spl-token "Permalink to this heading")
		
		[spl-token](https://spl.solana.com/token) is the Solana native way of creating tokens, minting, burning and transferring token. This is the Solana equivalent of [ERC-20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/) and [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/). Solang’s repository contains a library `SplToken` to use spl-token from Solidity. The file [spl_token.sol](https://github.com/hyperledger/solang/blob/main/solana-library/spl_token.sol) should be copied into your source tree, and then imported in your solidity files where it is required. The `SplToken` library has doc comments explaining how it should be used.
		
		There is an example in our integration tests of how this should be used. See [token.sol](https://github.com/hyperledger/solang/blob/main/integration/solana/token.sol) and [token.spec.ts](https://github.com/hyperledger/solang/blob/main/integration/solana/token.spec.ts).
		
		### System Instructions[](https://solang.readthedocs.io/en/latest/targets/solana.html#system-instructions "Permalink to this heading")
		
		Solana’s system instructions enable developers to interact with Solana’s System Program. There are functions to create new accounts, allocate account data, assign accounts to owning programs, transfer lamports from System Program owned accounts and pay transaction fees. More information about the functions offered can be found both on [Solana documentation](https://docs.rs/solana-program/1.11.10/solana_program/system_instruction/enum.SystemInstruction.html) and on Solang’s [system_instruction.sol](https://github.com/hyperledger/solang/blob/main/solana-library/system_instruction.sol) file.
		
		The usage of system instructions needs the correct setting of writable and signer accounts when interacting with Solidity contracts on chain. Examples are available on Solang’s integration tests. See [system_instruction_example.sol](https://github.com/hyperledger/solang/blob/main/integration/solana/system_instruction_example.sol) and [system_instruction.spec.ts](https://github.com/hyperledger/solang/blob/main/integration/solana/system_instruction.spec.ts)
		
		
		# Parity Substrate[](https://solang.readthedocs.io/en/latest/targets/substrate.html#parity-substrate "Permalink to this heading")
		
		Solang works with Parity Substrate 3.0. Note that for recent Substrate versions, cross-contract calls as well as using address type as function argument or return values are not supported. We are currently working on fixing any regressions.
		
		The Parity Substrate has the following differences to Ethereum Solidity:
		
		-   The address type is 32 bytes, not 20 bytes. This is what Substrate calls an “account”
		    
		-   An address literal has to be specified using the `address"5GBWmgdFAMqm8ZgAHGobqDqX6tjLxJhv53ygjNtaaAn3sjeZ"` syntax
		    
		-   ABI encoding and decoding is done using the [SCALE](https://docs.substrate.io/reference/scale-codec/) encoding
		    
		-   Constructors can be named. Constructors with no name will be called `new` in the generated metadata.
		    
		-   There is no `ecrecover()` builtin function, or any other function to recover or verify cryptographic signatures at runtime
		    
		-   Only functions called via rpc may return values; when calling a function in a transaction, the return values cannot be accessed
		    
		-   An assert(), require(), or revert() executes the wasm unreachable instruction. The reason code is lost
		    
		
		There is a solidity example which can be found in the [examples](https://github.com/hyperledger/solang/tree/main/examples) directory. Write this to flipper.sol and run:
		
		solang compile --target substrate flipper.sol
		
		Now you should have a file called `flipper.contract`. The file contains both the ABI and contract wasm. It can be used directly in the [Contracts UI](https://contracts-ui.substrate.io/), as if the contract was written in ink!.
		
		## Builtin Imports[](https://solang.readthedocs.io/en/latest/targets/substrate.html#builtin-imports "Permalink to this heading")
		
		Some builtin functionality is only available after importing. The following types can be imported via the special import file `substrate`.
		
		import {Hash} from 'substrate';
		import {chain_extension} from 'substrate';
		
		Note that `{Hash}` can be omitted, renamed or imported via import object.
		
		// Now Hash will be known as InkHash
		import {Hash as InkHash} from 'substrate';
		
		Note
		
		The import file `substrate` is only available when compiling for the Substrate target.
		
		# Brief Language status[](https://solang.readthedocs.io/en/latest/language/introduction.html#brief-language-status "Permalink to this heading")
		
		
		The Solidity language supported by Solang aims to be compatible with the latest [Ethereum Foundation Solidity Compiler](https://github.com/ethereum/solidity/), version 0.8 with some small exceptions.
		
		Note
		
		Where differences exist between different targets or the Ethereum Foundation Solidity compiler, this is noted in boxes like these.
		
		As with any new project, bugs are possible. Please report any issues you may find to github.
		
		Differences:
		
		-   libraries are always statically linked into the contract code
		    
		-   Solang generates WebAssembly or Solana SBF rather than EVM.
		    
		-   Packed encoded uses little endian encoding, as WASM and SBF are little endian virtual machines.
		    
		
		Unique features to Solang:
		
		-   Solang can target different blockchains and some features depending on the target. For example, Parity Substrate uses a different ABI encoding and allows constructors to be named.
		    
		-   Events can be declared outside of contracts
		    
		-   Base contracts can be declared in any order
		    
		-   There is a `print()` function for debugging
		    
		-   Strings can be formatted with python style format string, which is useful for debugging: `print("x = {}".format(x));`
		    
		-   Ethereum style address literals like `0xE0f5206BBD039e7b0592d8918820024e2a7437b9` are not supported on Substrate or Solana, but are supported for EVM.
		    
		-   On Substrate and Solana, base58 style encoded address literals like `address"5GBWmgdFAMqm8ZgAHGobqDqX6tjLxJhv53ygjNtaaAn3sjeZ"` are supported, but not with EVM.
		    
		-   On Solana, there is special builtin import file called `'solana'` available.
		    
		-   On Substrate, there is special builtin import file called `'substrate'` available.
		    
		-   Different blockchains offer different builtins. See the [builtins documentation](https://solang.readthedocs.io/en/latest/language/builtins.html#builtins).
		    
		-   There are many more differences, which are noted throughout the documentation.
- [[2023-05-23]]
- [[2023-05-24]]
- [[Hyperledger solang.canvas|Hyperledger solang]]