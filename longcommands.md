Install Command:
================
    
```docker exec cliMagnetoCorp peer chaincode install -n papercontract -v 0.0.3 -p /opt/gopath/src/github.com/contract -l node```
    
Instantiate Command:
====================
    
```docker exec cliMagnetoCorp peer chaincode instantiate -n papercontract -v 0.0.3 -l node -c '{"Args":["org.papernet.commercialpaper:instantiate"]}' -C mychannel -P "AND ('Org1MSP.member')"```
    
Get Paper - For Contract
========================
```
/**
* THIS IS FOR THE CONTRACT - NOT APPLICATION
* Get commercial paper
* @param {Context} ctx the transaction context
* @param {String} issuer commercial paper issuer
* @param {Integer} paperNumber paper number for this issuer
*/
async getPaper(ctx, issuer, paperNumber) {
try {
console.log("getPaper for: " + issuer + " " + paperNumber);
let paperKey = CommercialPaper.makeKey([issuer, paperNumber]);
let paper = await ctx.paperList.getPaper(paperKey);
return paper.toBuffer();
} catch(e) {
throw new Error('Paper does not exist' + issuer + paperNumber);
}
}
```
