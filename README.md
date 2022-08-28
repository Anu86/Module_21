# Application

## Challenge: Martian Token Crowdsale

You will create a fungible token that is ERC-20 compliant and that will be minted by using a `Crowdsale` contract from the OpenZeppelin Solidity library.

The crowdsale contract that you create will manage the entire crowdsale process, allowing users to send ether to the contract and in return receive KAI, or KaseiCoin tokens. Your contract will mint the tokens automatically and distribute them to buyers in one transaction.

### Instructions

The steps for this Challenge are divided into the following sections:

1. Create the KaseiCoin Token Contract
###### Please see Image 1 under Evaludation Evidence ###
    /*
    Constructor - Create contract with name, symbol and supply [ This indicates the supply the tokens]
    */
    constructor (
        string memory name,
        string memory symbol,
        uint supply
    ) 

2. Create the KaseiCoin Crowdsale Contract
###### Please see Image 2 under Evaludation Evidence ###
// Have the KaseiCoinCrowdsale contract inherit the following OpenZeppelin:
// * Crowdsale
// * MintedCrowdsale
// * CappedCrowdSale
// * TimedCrowdSale
// * RefundablePostDeliveryCrowdsale
contract KaseiCoinCrowdsale is Crowdsale, MintedCrowdsale, CappedCrowdsale, TimedCrowdsale, RefundablePostDeliveryCrowdsale { 
    // Provide parameters for all of the features of your crowdsale, such as the `rate`, `wallet` for fundraising, and `token`.
    constructor(
            uint rate,
            address payable issuer_wallet,
            KaseiCoin KaseiCoin_contract_addr,
            uint target,
            uint open,
            uint close
    ) public 
        Crowdsale (rate, issuer_wallet, KaseiCoin_contract_addr) 
        CappedCrowdsale (target)
        TimedCrowdsale (open, close)
        RefundableCrowdsale (target) {
            }
    
}

3. Create the KaseiCoin Deployer Contract
###### Please see Image 7 under Evaludation Evidence ###
contract KaseiCoinCrowdsaleDeployer {
    // Create an `address public` variable called `kasei_token_address`.
    address public kasei_token_address;
    
    // Create an `address public` variable called `kasei_crowdsale_address`.
    address public kasei_crowdsale_address;

    // Add the constructor.
    constructor(
       string memory name,
       string memory symbol,
       uint rate,
       address payable wallet,
       uint target
    ) public {
        // Create a new instance of the KaseiCoin contract.
        KaseiCoin token_contract = new KaseiCoin (name, symbol, 0);
        
        // Assign the token contract’s address to the `kasei_token_address` variable.
        kasei_token_address = address(token_contract);

        // Create a new instance of the `KaseiCoinCrowdsale` contract
        KaseiCoinCrowdsale crowdsale_contract = new KaseiCoinCrowdsale (rate, wallet, token_contract,target,now,now + 5 minutes);   
            
        // Aassign the `KaseiCoinCrowdsale` contract’s address to the `kasei_crowdsale_address` variable.
       kasei_crowdsale_address = address (crowdsale_contract);

        // Set the `KaseiCoinCrowdsale` contract as a minter
        token_contract.addMinter(kasei_crowdsale_address);
        
        // Have the `KaseiCoinCrowdsaleDeployer` renounce its minter role.
        token_contract.renounceMinter();
    }

4. Deploy the Crowdsale to a Local Blockchain
###### Please see Image 1, 2, 3, 4,5,6 ,7, 8 , 9 & Error scenarions under Evaludation Evidence ###


5. Optional: Extend the Crowdsale Contract by Using OpenZeppelin

#### Installation Guide 
1. Create a ganache accou t and view accoungt with 100 Ether each 
2. Compile KaseiCoin.sol 
3. Connect to Ganache by connecting to the  RPC server
4. Deploy KaseiCoin.sol -> Note the contract address it is deployed to 
4. Connect with Meta mask by import the Ganade account private key into Metamask 
5. Deploy contract and confirm deployment on metamask by defining the target, pen time & close time
6. Add minter address as needed by using contract function addminter 
7. Chcek if the role is granted
8. Compile kaseiCoinCrowdsale.sol 
9. Deploy contract and confirm deployment on metamask 
10. compile the deployer contract 
11. deploy the contract & verify the kaseiCoin wallet call & crwdsale address call 
12. Buy tokens & verify balance cap, goal 





