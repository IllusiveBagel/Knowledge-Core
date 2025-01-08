## 1. **Set Up a React Native Project with TypeScript**
First, create a new React Native project with TypeScript:
```base
npx react-native init MyReactNativeApp --template react-native-template-typescript
cd MyReactNativeApp
```
-
- ## 2. Install React Navigation
  :LOGBOOK:
  CLOCK: [2025-01-08 Wed 13:08:49]
  :END:
  Install the required dependencies for **react-navigation**:
  ```bash
  npm install @react-navigation/native
  npm install react-native-screens react-native-safe-area-context react-native-gesture-handler react-native-reanimated react-native-vector-icons
  ```
  Install the **stack navigator** for screen navigation:
  ```bash
  npm install @react-navigation/stack
  ```
  Install TypeScript types for React Navigation and React:
  ```bash
  npm install --save-dev @types/react @types/react-native @react-navigation/native @react-navigation/stack
  ```
- ## 3. Set Up the Navigation
  Create a basic folder structure:
  ```css
  src/
    components/
    navigation/
      AppNavigator.tsx
    screens/
      LoginScreen.tsx
      HomeScreen.tsx
  ```
  Configure `AppNavigator.tsx`
  Create a `AppNavigator.tsx` file under the `navigation` folder:
  
  ```tsx
  import React from "react";
  import { NavigationContainer } from "@react-navigation/native";
  import { createStackNavigator } from "@react-navigation/stack";
  import LoginScreen from "../screens/LoginScreen";
  import HomeScreen from "../screens/HomeScreen";
  
  export type RootStackParamList = {
    Login: undefined;
    Home: undefined;
  };
  
  const Stack = createStackNavigator<RootStackParamList>();
  
  const AppNavigator: React.FC = () => {
    return (
      <NavigationContainer>
        <Stack.Navigator initialRouteName="Login">
          <Stack.Screen name="Login" component={LoginScreen} />
          <Stack.Screen name="Home" component={HomeScreen} />
        </Stack.Navigator>
      </NavigationContainer>
    );
  };
  
  export default AppNavigator;
  ```