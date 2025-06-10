# REACT-Redux-example

//FIRST DEFINE INITIAL STATE
     
                const initialWagonState = {
                  supplies: 100,
                  distance: 0,
                  days: 0,
                  //13.Add a cashProperty
                  cash: 200,
                }

//SECOND DEFINE A REDUCER TO MANAGE STATE

          const stateReducer = (state = initialWagonState, action) => {
               
//THIRD.A. HELP REDUCER DECIDE WHAT THE STATE SHOULD BE WITH SWITCH STATEMENTS </BR>
//FOUR MAKE THE FIRST CASE for gathering supplies for a trip</BR>

           	 switch(action.type){
                     case'gather':{
                     	return {
        	     // use spread operator to add old state then update to new with only things that change... supplies and days.
                       		...state,
                         	supplies: state.supplies+15,
                          	days: state.days + 1
           		       }
       	            }
// FIVE ADD AN action.type for 'travel' based on number of days a player wants to travel

                     case 'travel': {
                        const days = action.payload;
                        //12. Add conditional for case when supplies become negative
                        const newSupplies = state.supplies - (20*days);
                        if(newSupplies < 0 ){
                          return state;
                          // `Can't travel Not enough Supplies`;
                        } 
                          return {
                            ...state,
                            //12.not negative case supplies like this okay
                            //  supplies:state.supplies - (20*days),
                             supplies: newSupplies,
                             distance: state.distance + (10*days),
                             days: state.days + days,
                          }
                        }
// SIX ADD an action.type for 'tippedwagon' if the wagon tips over during travel

                   case'tippedWagon':{
                     return {
                       ...state,
                       supplies: state.supplies - 30,
                       distance: state.distance,
                       days: state.days + 1,
                     }
                   }
//13.b.Add a sell case

                   case 'sell': {
                     const sellSupplies = state.supplies -20;
                     if(sellSupplies < 0 ){ 
                       return state;
                       }
                     return {
                       ...state,
                       supplies: state.supplies -20,
                       cash: state.cash + 5,
                     }
                   }
//13. EXTRAS c.BUY d.THEFT AND FILL UP AGAIN

                 case "fill up":{
                   return {
                     ...state,
                     supplies: state.supplies + 200
                   }
                 }
                 case "buy":{
                   return {
                     ...state,
                     supplies: state.supplies + 25,
                     cash: state.cash - 15,
                   }
                 }
                 case "theft":{
                   return {
                     ...state,
                     cash: state.cash/2,
                   }
                 }
//THIRD START WITH A DEFAULT CASE IF NO MATCH FOUND.

               default: {
                     	return state;
                  	 }
            }
          }
|QUESTION | INSTRUCTION | STORED STATE FUNCTION CALL  | ******* CONSOLE.LOG ******* |
| ------------- | ------------- | ------------- | ------------- |
|7|Play the game call the reducer with state=undefined action=empty... continue to store|let wagon = stateReducer(undefined, {}); |console.log('Default: ',wagon);|
|8|Day 1 Call reducer to travel this day with state=wagon action type=travel actionpayload/day = 1 |wagon = stateReducer(wagon, {type:'travel', payload:1});|console.log('Trip 1: ', wagon);|
|9|Day2 Call reducer to stop and gather state=wagon action.type=gather no action.payload|wagon = stateReducer(wagon, {type:'gather'});|console.log('Trip 2: ',wagon);|
|10| Day3 The wagon tips over in a river call reducer with current state wagon and action.type = tippedwagon|wagon = stateReducer(wagon, {type:'tippedWagon'});|console.log('Trip 3: ',wagon)|
|11|3 Day travel so call reducer with current wagon state and action.type='travel' and action.payload=3 days of travel|wagon = stateReducer(wagon, {type:'travel', payload:3});|console.log('Trip 4: ',wagon);|
|12|Use Test case if we continue to travel even if supplies are negative|wagon = stateReducer(wagon, {type:'travel', payload:3});|console.log('Trip 5: ',wagon);|
|X|Extra: lets stop and fill up our reserves |wagon = stateReducer(wagon, {type:'fill up'});|console.log('Fill up: ',wagon)|
##### =========================================================================================			                                   
|13. QUESTION EXTRAS  | STORED STATE FUNCTION CALL  | CONSOLE.LOG |
| ------------- | ------------- | --- |
|13.a.Add a cash property|| |
|13.b. Add a 'sell' Case | wagon = stateReducer(wagon, {type:'sell'}); |console.log('Sell For Cash: ',wagon); |
|13.c.Add a 'buy' case  | wagon = stateReducer(wagon, {type:'buy'}); | console.log('Buy to gain supplies: ',wagon); |   
|13.d.Add a 'theft' case| wagon = stateReducer(wagon, {type:'theft'}); |console.log('Theft of cash: ',wagon); |
 

		 							
 									
							

