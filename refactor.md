## Refactor Documentation

### Overview

This documentation provides a step-by-step guide for refactoring a React Native app. The goal of this refactoring process is to enhance code quality, improve performance, and make the application more maintainable.

```js
const  ClickHandler  = ({ id, getState }) => {

const  handleClick  =  useCallback(() => {

getState(id);

}, [id]);

  

return (

<View>

<Text>

<Button  title="Click"  onPress={handleClick}  />

</Text>

</View>

);

};

  

const  RenderHandlingUseMemo  = ({ data }) => {

const  displayList  =  useMemo(() => {

return  data.map((item) => {

return (

<View  key={item.id}>

<Text>{item.label}</Text>

</View>

);

});

}, [data]);

return  <View>{displayList}</View>;

};

  

const  ItemComponent  = ({ label }) => {

return (

<View>

<Text>{label}</Text>

</View>

);

};

const  RenderHandlingComponent  = ({ data }) => {

return (

<View>

{data.map((item) => (

<ItemComponent  key={item.id}  label={item.label}  />

))}

</View>

);

};

  

/**

* instead of making persist individual variables those are use to manage app

* initial state save it in single state as appConfig Object and save it in AsyncStorage

* this will reduce the number of AsyncStorage calls and app will load faster

*/

const  AppConfig  = {

UserId:  "1343oujo2343o434uljfs",

username:  "iswan.jumat",

schoolCode:  "schoolLocal",

};

// @ts-expect-error

await  AsyncStorage.setItem("appConfig", JSON.stringify(AppConfig));

// @ts-expect-error

_globalState.setAppConfig(AppConfig);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4OTk0MjMwLC04NjYyMDk3ODksLTEwND
YyNzg3MjZdfQ==
-->