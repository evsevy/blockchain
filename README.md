# blockchain
smart code
contract Bank {
    address owner;
    mapping(address => uint) balances;
    
    function Bank() {
        owner = msg.sender;
    }

    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    function withdraw(uint amount) public {
        if (balances[msg.sender] >= amount) {
            balances[msg.sender] -= amount;
            msg.sender.transfer(amount);
        }
    }

    function getMyBalance() public view returns(uint) {
        return balances[msg.sender];
    }

    function kill() public {
        if (msg.sender == owner)
            selfdestruct(owner);
    }
}
