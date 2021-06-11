# react-redux-project-steps

## Install redux and react-redux
``` 
  npm i redux react-redux
```
## Create directories
1. Action
2. components
3. Data
4. Pages
5. Reducers

## Create reducers 
Inside reducer folder create all the needed reducers and index.js (this will have root reducer which is over data store like state)
reducers are functions which takes two arguments 'Previous state' and 'Action'.
 ### Sample reducer
```
import StoreData from '../Data/shop.data';
const initialData= {StoreData:StoreData}
const storeDataReducer = (state=initialData,action) =>{
  switch(action.type){
    case '--------':
      return 'modified state';
    default:
      return state;
  }
}
export default storeDataReducer;
```
### Sample root reducer i.e index.js inside reducer folder
```
import storeDataReducer from './storeData.reducers';

import {combineReducers} from 'redux';

const RootReducer =  combineReducers({
  store:storeDataReducer

})
export default RootReducer
```

### Now create store in src/index.js using RootReducer
``` 
import rootReducer from './Reducers/index';
import {createStore} from 'redux';
import { Provider } from 'react-redux';

const store = createStore(rootReducer,window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
          <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```
### Now start creating components 
### Now as required start creating Actions 
Create file called index.js in Action Folder.
Now create individual actions as shown below.
```
export const LoadCovinPinData =(data)=>{
    return {
        type:'LOAD_COVINPIN_DATA',
        payload: data
    }
}
export const LoadCovinDistData =(data)=>{
    return {
        type:'LOAD_COVINDIST_DATA',
        payload: data
    }
}
```
### Now Dispatch the action from required component and don't forget to put it in case statment of concern reducer.
```
import {useEffect} from 'react';
import {useDispatch,useSelector} from 'react-redux'
import {LoadCovinPinData}from '../Actions';

const CovinPin = () => {
    const dispatch = useDispatch()
    useEffect(() => {
        fetch('https://cdn-api.co-vin.in/api/v2/appointment/sessions/public/findByPin?pincode=396050&date=10-06-2021')
        .then(response => response.json())
        .then(data =>dispatch(LoadCovinPinData(data.sessions)));
      },[]);

    const dataPin = useSelector(state=>state.covinPinReducer)
   
    return (
        <div>
          { dataPin.covinPin.map(el=>(<p>{el.min_age_limit}</p>))}
        </div>
    )
}
export default CovinPin
```
========================================================================
<br>Updated reducer code with action type.
```
const InitialState = [];
const covinPinReducer =(state=InitialState,action)=>{
    switch (action.type) {
        case 'LOAD_COVINPIN_DATA':
            return {covinPin:action.payload}
        default:
            return state;
    }
}
export default covinPinReducer;
```
