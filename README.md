# Deterministic 
## Smart contracts are deterministic  same input = same output 
- A deterministic smart contract is a contract in which the same inputs always produce the same outputs, no matter when or where the contract is executed. Determinism is crucial in smart contracts to ensure consistency, predictability, and trust across all Ethereum nodes in the network
- Consistency Across Nodes: All Ethereum nodes running the contract reach the same result when processing the same transaction. This is vital for consensus.

![Static Badge](https://img.shields.io/badge/Randomness%20Teat%201%20-Green)

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.28;

contract randomnessTest1 {

    function deterministicFunction(uint256 addNumber) public pure returns(uint256) {
        uint256 randomnessNumber;
      return randomnessNumber = addNumber*2;
    }   
}
```

 Script to deploy
 
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import {Script, console} from "forge-std/Script.sol";
import {randomnessTest1} from "../src/randomnessTest1.sol";

contract DeployRandomnessTest1 is Script {
    randomnessTest1 public randomnesstest1;

    function setUp() public {}
    function run() public {
        vm.startBroadcast();
        randomnesstest1 = new randomnessTest1();
        vm.stopBroadcast();
    }
}
```

 Test Foundry
 
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.28;

import {Test, console} from "forge-std/Test.sol";
import {randomnessTest1} from "../src/randomnessTest1.sol";

contract CounterTest is Test {
    randomnessTest1 public randomnesstest1;
    function setUp() public {
         randomnesstest1 = new randomnessTest1();
    }
    // Test deterministicFunction with a specific input
    function testDeterministicFunction() public view {
        uint256 addNumber = 5;
        uint256 expectedResult = 10;
        assertEq(randomnesstest1.deterministicFunction(addNumber),expectedResult);
    }
    // Test deterministicFunction with a large input
    function testDeterministicFunctionLargeInput() public view {
        uint256 addNumber = type(uint256).max/2;
        uint256 expectedResult = addNumber*2;
        assertEq(randomnesstest1.deterministicFunction(addNumber),expectedResult);        
}
}
```
