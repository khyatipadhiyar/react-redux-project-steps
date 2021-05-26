# react-redux-project-steps
## create directories
1. Action
2. components
3. Data
4. Pages
5. Reducers

## create reducers 
Inside reducer folder create all the needed reducers and index.js (this will have root reducer which is over data store like state)
reducers are functions which takes two arguments 'Previous state' and 'Action'.
 ### Sample reducer
 ### `const initialData= {StoreData:StoreData}

const storeDataReducer = (state=initialData,action) =>{
  switch(action.type){
    default:
      return state;
  }
}
export default storeDataReducer;`

