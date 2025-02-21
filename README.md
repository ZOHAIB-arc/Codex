

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Import OpenZeppelin's ERC20 implementation
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract CodexToken is ERC20 {
    // Variable to store the development type (AI-developed or self-developed)
    string public developmentType;

    // Constructor to initialize the token
    constructor(
        string memory _name,
        string memory _symbol,
        uint256 _initialSupply,
        string memory _devType
    ) ERC20(_name, _symbol) {
        // Mint initial supply to the deployer's address
        _mint(msg.sender, _initialSupply * 10 ** decimals());

        // Set the development type
        developmentType = _devType;
    }

    // Function to check if the token is AI-developed or self-developed
    function getDevelopmentType() public view returns (string memory) {
        return developmentType;
    }

    // Function to make the code easy to understand (example)
    function explainCode() public pure returns (string memory) {
        return "This is the Codex token. It helps you understand if the code is AI-developed or self-developed. Use getDevelopmentType() to check.";
    }
}
const hre = require("hardhat");

async function main() {
  const [deployer] = await hre.ethers.getSigners();
  console.log("Deploying contracts with account:", deployer.address);

  const CodexToken = await hre.ethers.getContractFactory("CodexToken");
  const codexToken = await CodexToken.deploy("Codex", "CDX", 1000000, "AI-Developed");

  console.log("Waiting for deployment...");
  await codexToken.deployed();

  console.log("CodexToken deployed to:", codexToken.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error("Deployment failed:", error);
    process.exit(1);
  });
