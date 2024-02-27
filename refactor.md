## Refactor Documentation

### Overview

This documentation provides a step-by-step guide for refactoring a React Native app. The goal of this refactoring process is to enhance code quality, improve performance, and make the application more maintainable.

### Usage of `useCallback` hook

The use of useCallback in the ClickHandler component is a best practice that optimizes performance by memoizing the handleClick function. This ensures that the function is recreated only if the id prop changes, preventing unnecessary renders and promoting efficient rendering in React components.

```js
const ClickHandler = ({ id, getState }) => {
  const handleClick = useCallback(() => {
    getState(id);
  }, [id]);

  return (
    <View>
      <Button title="Click" onPress={handleClick} />
    </View>
  );
};
```

### Usage of `useMemo`

In the RenderHandlingUseMemo component, the use of useMemo is a best practice to optimize performance. By memoizing the displayList array, it prevents the creation of brand new React components on every rerender. This is achieved by specifying the data prop in the dependency array, ensuring efficient rendering and enhancing performance, particularly in scenarios involving lists or arrays of elements.

```js
const RenderHandlingUseMemo = ({ data }) => {
  const displayList = useMemo(() => {
    return data.map((item) => {
      return (
        <View key={item.id}>
          <Text>{item.label}</Text>
        </View>
      );
    });
  }, [data]);
  return <View>{displayList}</View>;
};
```

### Avoid Inline Render Methods Inside Another Component.

**_Avoid_**

```js
const RenderHandlingComponent = ({ data }) => {
  return (
    <View>
      {data.map((item) => (
        <View key={item.id}>
          <Text>{item.label}</Text>
        </View>
      ))}
    </View>
  );
};
```

Above code will create a brand new react component in very rerender of RenderHandlingComponent which is a bad practice.

**_Prefer_**

```js
const ItemComponent = ({ label }) => {
  return (
    <View>
      <Text>{label}</Text>
    </View>
  );
};

const RenderHandlingComponent = ({ data }) => {
  return (
    <View>
      {data.map((item) => (
        <ItemComponent key={item.id} label={item.label} />
      ))}
    </View>
  );
};
```

This approach separates the rendering of individual items into the reusable ItemComponent, mitigating the creation of new components on every rerender of RenderHandlingComponent.

### Saving Local Storage Data

Instead of persisting individual variables <I>(except auth tokens) </I> that are used to manage the app's initial state, consolidate them into a single state object named `appConfig`. Storing this object in AsyncStorage will reduce the number of calls to AsyncStorage, resulting in a faster app loading time.

```js
const AppConfig = {
  UserId: "1343oujo2343o434uljfs",
  username: "iswan.jumat",
  schoolCode: "schoolLocal",
};

await AsyncStorage.setItem("appConfig", JSON.stringify(AppConfig));

_globalState.setAppConfig(AppConfig);
```
