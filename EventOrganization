//SPDX-License-Identifier: Unlicense
pragma solidity >=0.5.0 <0.9.0;


contract EventContract {
 struct Event{
   address organizer;
   string name;
   uint date; 
   uint price;
   uint ticketCount;  
   uint ticketRemain;
 }

 uint public nextId;
 mapping(uint=>Event) public events;
 mapping(address=>mapping(uint=>uint)) public tickets;

 


 function createEvent(string memory name,uint date,uint price,uint ticketCount) external{
   require(date>block.timestamp,"Please select a future date for the event");
   require(ticketCount>0,"the number of tickets should be greater than zero for organizing a event");


   events[nextId] = Event(msg.sender,name,date,price,ticketCount,ticketCount);
   nextId++;
 }


 function buyTicket(uint id,uint quantity) external payable{
   require(events[id].date!=0,"Event does not exist");
   require(events[id].date>block.timestamp,"Event has already occured");
   Event storage _event = events[id];
   require(msg.value==(_event.price*quantity),"Ethere is not enough");
   require(_event.ticketRemain>=quantity,"Not enough tickets");
   _event.ticketRemain-=quantity;
   tickets[msg.sender][id]+=quantity;


 }


 function transferTicket(uint id,uint quantity,address to) external{
   require(events[id].date!=0,"Event does not exist");
   require(events[id].date>block.timestamp,"Event has already occured");
   require(tickets[msg.sender][id]>=quantity,"You do not have enough tickets");
   tickets[msg.sender][id]-=quantity;
   tickets[to][id]+=quantity;
 }
}
