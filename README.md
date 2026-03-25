# Access-Control
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AccessControl {
    address public admin;
    mapping(address => bool) public moderators;

    constructor() {
        admin = msg.sender;
    }

    modifier onlyAdmin() {
        require(msg.sender == admin, "Only admin");
        _;
    }

    function addModerator(address mod) public onlyAdmin {
        moderators[mod] = true;
    }

    function removeModerator(address mod) public onlyAdmin {
        moderators[mod] = false;
    }

    function restrictedFunction() public {
        require(moderators[msg.sender] || msg.sender == admin, "No permission");
        // code here
    }
}
