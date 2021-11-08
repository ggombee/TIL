# bottomModal 공통으로 사용하기

```jsx
import React from "react";
import {
  Alert,
  StatusBar,
  StyleSheet,
  Text,
  TouchableOpacity,
  useWindowDimensions,
  View,
} from "react-native";
import Modal from "react-native-modal";
import { useSafeAreaInsets } from "react-native-safe-area-context";
import colors from "#common/colors";

const BottomModal = ({
  onBackdropPress,
  isVisible,
  children,
  style,
  buttonText,
  ...rest
}) => {
  // console.log(children);
  const insets = useSafeAreaInsets();
  const { width } = useWindowDimensions();

  return (
    <Modal
      isVisible={isVisible}
      onBackdropPress={onBackdropPress}
      style={[styles.wrapper, style]}
      {...rest}
    >
      <View
        style={[
          {
            width,
            paddingBottom: insets.bottom,
          },
          styles.bottomSheet,
        ]}
      >
        <View style={styles.notchWrapper}>
          <View style={styles.notch} />
        </View>
        {children}
      </View>
      <TouchableOpacity
        style={{
          backgroundColor: colors.primary,
          paddingBottom: insets.bottom,
          height: 77,
          paddingTop: 20,
          justifyContent: "center",
        }}
      >
        <Text style={styles.bottomText}>{buttonText}</Text>
      </TouchableOpacity>
    </Modal>
  );
};

export default BottomModal;

const styles = StyleSheet.create({
  wrapper: {
    padding: 0,
    justifyContent: "flex-end",
    margin: 0,
  },
  bottomSheet: {
    backgroundColor: "white",
    borderTopLeftRadius: 15,
    borderTopRightRadius: 15,
  },
  notchWrapper: {
    height: 30,
    justifyContent: "center",
    alignItems: "center",
  },
  notch: {
    height: 5,
    borderRadius: 2.5,
    width: 80,
    backgroundColor: "#f0f0f0",
  },
  defaultHeight: {
    minHeight: 200,
  },
  bottomText: {
    fontSize: 16,
    fontWeight: "500",
    fontStyle: "normal",
    lineHeight: 19,
    letterSpacing: -0.8,
    textAlign: "center",
    color: colors.white,
  },
});
```
