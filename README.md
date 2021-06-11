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

