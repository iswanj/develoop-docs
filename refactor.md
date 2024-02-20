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
			<Button  title="Click"  onPress={handleClick}  />
		</View>
	);
};
```

```js

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
```

```js
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
				<ItemComponent  key={item.id}  label=		{item.label}  />
			))}
		</View>
	);
};
```
#### Saving Local Storage Data
Instead of persisting individual variables ***<I>(except auth tokens) </I>*** that are used to manage the app's initial state, consolidate them into a single state object named `appConfig`. Storing this object in AsyncStorage will reduce the number of calls to AsyncStorage, resulting in a faster app loading time.
```js
const  AppConfig  = {
	UserId:  "1343oujo2343o434uljfs",
	username:  "iswan.jumat",
	schoolCode:  "schoolLocal",
};

await  AsyncStorage.setItem("appConfig", JSON.stringify(AppConfig));

_globalState.setAppConfig(AppConfig);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MjIyOTQ1OTVdfQ==
-->