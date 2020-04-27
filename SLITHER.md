INFO:Detectors:
SmartMatrixForsage.sendETHDividends(address,address,uint8,uint8) (SmartMatrixForsage.sol#435-445) sends eth to arbitrary user
        Dangerous calls:
        - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
        - address(uint160(receiver)).transfer(address(this).balance) (SmartMatrixForsage.sol#439)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations

INFO:Detectors:
SmartMatrixForsage.registration(address,address) (SmartMatrixForsage.sol#152-190) uses assembly
        - INLINE ASM None (SmartMatrixForsage.sol#158-160)
SmartMatrixForsage.bytesToAddress(bytes) (SmartMatrixForsage.sol#447-451) uses assembly
        - INLINE ASM None (SmartMatrixForsage.sol#448-450)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage
INFO:Detectors:
Different versions of Solidity is used in :
        - Version used: ['>=0.4.21<0.7.0', '>=0.4.23<0.6.0']
        - >=0.4.23<0.6.0 (SmartMatrixForsage.sol#26)
        - >=0.4.21<0.7.0 (Migrations.sol#1)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version>=0.4.23<0.6.0 (SmartMatrixForsage.sol#26) allows old versions
Pragma version>=0.4.21<0.7.0 (Migrations.sol#1) allows old versions
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Parameter SmartMatrixForsage.findEthReceiver(address,address,uint8,uint8)._from (SmartMatrixForsage.sol#409) is not in mixedCase
Parameter SmartMatrixForsage.sendETHDividends(address,address,uint8,uint8)._from (SmartMatrixForsage.sol#435) is not in mixedCase
Variable Migrations.last_completed_migration (Migrations.sol#5) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Reentrancy in SmartMatrixForsage.buyNewLevel(uint8,uint8) (SmartMatrixForsage.sol#116-150):
        External calls:
        - updateX3Referrer(msg.sender,freeX3Referrer,level) (SmartMatrixForsage.sol#132)
                - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
                - address(uint160(receiver)).transfer(address(this).balance) (SmartMatrixForsage.sol#439)
        Event emitted after the call(s):
        - Upgrade(msg.sender,freeX3Referrer,1,level) (SmartMatrixForsage.sol#134)
Reentrancy in SmartMatrixForsage.buyNewLevel(uint8,uint8) (SmartMatrixForsage.sol#116-150):
        External calls:
        - updateX6Referrer(msg.sender,freeX6Referrer,level) (SmartMatrixForsage.sol#146)
                - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
                - address(uint160(receiver)).transfer(address(this).balance) (SmartMatrixForsage.sol#439)
        Event emitted after the call(s):
        - Upgrade(msg.sender,freeX6Referrer,2,level) (SmartMatrixForsage.sol#148)
Reentrancy in SmartMatrixForsage.registration(address,address) (SmartMatrixForsage.sol#152-190):
        External calls:
        - updateX3Referrer(userAddress,freeX3Referrer,1) (SmartMatrixForsage.sol#185)
                - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
                - address(uint160(receiver)).transfer(address(this).balance) (SmartMatrixForsage.sol#439)
        - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
                - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
                - address(uint160(receiver)).transfer(address(this).balance) (SmartMatrixForsage.sol#439)
        State variables written after the call(s):
        - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
                - users[users[referrerAddress].x6Matrix[level].firstLevelReferrals[0]].x6Matrix[level].firstLevelReferrals.push(userAddress) (SmartMatrixForsage.sol#310)
                - users[referrerAddress].x6Matrix[level].firstLevelReferrals.push(userAddress) (SmartMatrixForsage.sol#229)
                - users[userAddress].x6Matrix[level].currentReferrer = users[referrerAddress].x6Matrix[level].firstLevelReferrals[0] (SmartMatrixForsage.sol#314)
                - users[userAddress].x6Matrix[level].currentReferrer = referrerAddress (SmartMatrixForsage.sol#233)
                - users[users[referrerAddress].x6Matrix[level].firstLevelReferrals[1]].x6Matrix[level].firstLevelReferrals.push(userAddress) (SmartMatrixForsage.sol#316)
                - users[users[referrerAddress].x6Matrix[level].currentReferrer].x6Matrix[level].closedPart = referrerAddress (SmartMatrixForsage.sol#334)
                - users[userAddress].x6Matrix[level].currentReferrer = users[referrerAddress].x6Matrix[level].firstLevelReferrals[1] (SmartMatrixForsage.sol#320)
                - users[ref].x6Matrix[level].secondLevelReferrals.push(userAddress) (SmartMatrixForsage.sol#240)
                - users[users[referrerAddress].x6Matrix[level].currentReferrer].x6Matrix[level].closedPart = referrerAddress (SmartMatrixForsage.sol#337)
                - users[referrerAddress].x6Matrix[level].firstLevelReferrals = new address[](0) (SmartMatrixForsage.sol#342)
                - users[referrerAddress].x6Matrix[level].secondLevelReferrals = new address[](0) (SmartMatrixForsage.sol#343)
                - users[referrerAddress].x6Matrix[level].closedPart = address(0) (SmartMatrixForsage.sol#344)
                - users[referrerAddress].x6Matrix[level].blocked = true (SmartMatrixForsage.sol#347)
                - users[referrerAddress].x6Matrix[level].reinvestCount ++ (SmartMatrixForsage.sol#350)
                - users[referrerAddress].x6Matrix[level].secondLevelReferrals.push(userAddress) (SmartMatrixForsage.sol#270)
        Event emitted after the call(s):
        - MissedEthReceive(receiver,_from,1,level) (SmartMatrixForsage.sol#415)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - MissedEthReceive(receiver,_from,2,level) (SmartMatrixForsage.sol#425)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,users[referrerAddress].x6Matrix[level].firstLevelReferrals[0],2,level,uint8(users[users[referrerAddress].x6Matrix[level].firstLevelReferrals[0]].x6Matrix[level].firstLevelReferrals.length)) (SmartMatrixForsage.sol#311)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,referrerAddress,2,level,uint8(users[referrerAddress].x6Matrix[level].firstLevelReferrals.length)) (SmartMatrixForsage.sol#230)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,referrerAddress,2,level,2 + uint8(users[users[referrerAddress].x6Matrix[level].firstLevelReferrals[0]].x6Matrix[level].firstLevelReferrals.length)) (SmartMatrixForsage.sol#312)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,users[referrerAddress].x6Matrix[level].firstLevelReferrals[1],2,level,uint8(users[users[referrerAddress].x6Matrix[level].firstLevelReferrals[1]].x6Matrix[level].firstLevelReferrals.length)) (SmartMatrixForsage.sol#317)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,referrerAddress,2,level,4 + uint8(users[users[referrerAddress].x6Matrix[level].firstLevelReferrals[1]].x6Matrix[level].firstLevelReferrals.length)) (SmartMatrixForsage.sol#318)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,ref,2,level,5) (SmartMatrixForsage.sol#248)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,ref,2,level,6) (SmartMatrixForsage.sol#250)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,ref,2,level,3) (SmartMatrixForsage.sol#255)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,ref,2,level,4) (SmartMatrixForsage.sol#257)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,ref,2,level,5) (SmartMatrixForsage.sol#261)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - NewUserPlace(userAddress,ref,2,level,6) (SmartMatrixForsage.sol#263)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - Registration(userAddress,referrerAddress,users[userAddress].id,users[referrerAddress].id) (SmartMatrixForsage.sol#189)
        - Reinvest(referrerAddress,freeReferrerAddress,userAddress,2,level) (SmartMatrixForsage.sol#355)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - Reinvest(owner,address(0),userAddress,2,level) (SmartMatrixForsage.sol#358)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
        - SentExtraEthDividends(_from,receiver,matrix,level) (SmartMatrixForsage.sol#443)
                - updateX6Referrer(userAddress,findFreeX6Referrer(userAddress,1),1) (SmartMatrixForsage.sol#187)
Reentrancy in SmartMatrixForsage.sendETHDividends(address,address,uint8,uint8) (SmartMatrixForsage.sol#435-445):
        External calls:
        - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
        Event emitted after the call(s):
        - SentExtraEthDividends(_from,receiver,matrix,level) (SmartMatrixForsage.sol#443)
Reentrancy in SmartMatrixForsage.updateX3Referrer(address,address,uint8) (SmartMatrixForsage.sol#192-223):
        External calls:
        - sendETHDividends(owner,userAddress,1,level) (SmartMatrixForsage.sol#219)
                - ! address(uint160(receiver)).send(levelPrice[level]) (SmartMatrixForsage.sol#438)
                - address(uint160(receiver)).transfer(address(this).balance) (SmartMatrixForsage.sol#439)
        State variables written after the call(s):
        - users[owner].x3Matrix[level].reinvestCount ++ (SmartMatrixForsage.sol#220)
        Event emitted after the call(s):
        - Reinvest(owner,address(0),userAddress,1,level) (SmartMatrixForsage.sol#221)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-4
INFO:Detectors:
usersActiveX3Levels(address,uint8) should be declared external:
        - SmartMatrixForsage.usersActiveX3Levels(address,uint8) (SmartMatrixForsage.sol#383-385)
usersActiveX6Levels(address,uint8) should be declared external:
        - SmartMatrixForsage.usersActiveX6Levels(address,uint8) (SmartMatrixForsage.sol#387-389)
usersX3Matrix(address,uint8) should be declared external:
        - SmartMatrixForsage.usersX3Matrix(address,uint8) (SmartMatrixForsage.sol#391-395)
usersX6Matrix(address,uint8) should be declared external:
        - SmartMatrixForsage.usersX6Matrix(address,uint8) (SmartMatrixForsage.sol#397-403)
setCompleted(uint256) should be declared external:
        - Migrations.setCompleted(uint256) (Migrations.sol#15-17)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#public-function-that-could-be-declared-as-external