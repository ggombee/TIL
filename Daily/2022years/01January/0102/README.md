# RN 스위치 컴포넌트를 직접 구현해보자!

### 스위치 컴포넌트 부르는곳

```jsx
<View style={styles.menuContainer}>
  <TouchableOpacity
    activeOpacity={1}
    style={styles.menuItem}
    onPress={() => setReceivePush((x) => !x)}
  >
    <Text style={styles.menuText}>푸시알림 허용</Text>
    <Switch checked={receivePush} />
  </TouchableOpacity>
  <View style={styles.line} />
</View>
```

### Switch.js

```jsx
import React, { useEffect } from "react";
import Animated, {
  timing,
  useAnimatedScrollHandler,
  useAnimatedStyle,
  useSharedValue,
  withTiming,
} from "react-native-reanimated";
import { StyleSheet, Text, TouchableOpacity, View, Image } from "react-native";

const styles = StyleSheet.create({
  toggleContainer: {
    width: 50,
    height: 30,
    paddingLeft: 2,
    borderRadius: 15,
    justifyContent: "center",
    backgroundColor: "#E8E8E8",
  },
  background: {
    backgroundColor: "#246DFB",
    position: "absolute",
    width: 50,
    height: 30,
    borderRadius: 15,
  },
  toggleWheel: {
    width: 25,
    height: 25,
    backgroundColor: "white",
    borderRadius: 12.5,
    shadowColor: "#000",
    shadowOffset: {
      width: 0,
      height: 2,
    },
    shadowOpacity: 0.2,
    shadowRadius: 2.5,
    elevation: 1.5,
  },
});

const Switch = ({ checked, onPress }) => {
  const data = useSharedValue(0);
  const style = useAnimatedStyle(() => {
    return {
      transform: [{ translateX: (data.value / 100) * 21 }],
    };
  }, []);
  const style2 = useAnimatedStyle(() => {
    return {
      opacity: data.value / 100,
    };
  }, []);

  useEffect(() => {
    data.value = withTiming(checked ? 100 : 0, {
      duration: 200,
    });
  }, [checked]);

  return (
    <TouchableOpacity
      activeOpacity={1}
      onPress={onPress}
      style={[styles.toggleContainer, { backgroundColor: "#E8E8E9" }]}
    >
      <Animated.View style={[styles.background, style2]} />
      <Animated.View style={[styles.toggleWheel, style]} />
    </TouchableOpacity>
  );
};

export default Switch;
```
