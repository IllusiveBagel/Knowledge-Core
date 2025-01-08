## 1. **Set Up a React Native Project with TypeScript**
First, create a new React Native project with TypeScript:
```bash
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
- ## 4. Create Login and Home Screens
  Create `LoginScreen.tsx`
  Define a basic login screen:
  
  ```tsx
  import React, { useState } from "react";
  import { View, Text, TextInput, Button, StyleSheet } from "react-native";
  import { StackNavigationProp } from "@react-navigation/stack";
  import { RootStackParamList } from "../navigation/AppNavigator";
  
  type LoginScreenNavigationProp = StackNavigationProp<RootStackParamList, "Login">;
  
  type Props = {
    navigation: LoginScreenNavigationProp;
  };
  
  const LoginScreen: React.FC<Props> = ({ navigation }) => {
    const [username, setUsername] = useState("");
    const [password, setPassword] = useState("");
  
    const handleLogin = () => {
      if (username && password) {
        navigation.replace("Home");
      } else {
        alert("Please enter valid credentials.");
      }
    };
  
    return (
      <View style={styles.container}>
        <Text style={styles.title}>Login</Text>
        <TextInput
          style={styles.input}
          placeholder="Username"
          value={username}
          onChangeText={setUsername}
        />
        <TextInput
          style={styles.input}
          placeholder="Password"
          secureTextEntry
          value={password}
          onChangeText={setPassword}
        />
        <Button title="Login" onPress={handleLogin} />
      </View>
    );
  };
  
  const styles = StyleSheet.create({
    container: { flex: 1, justifyContent: "center", padding: 16 },
    title: { fontSize: 24, marginBottom: 16, textAlign: "center" },
    input: { borderWidth: 1, marginBottom: 16, padding: 8, borderRadius: 4 },
  });
  
  export default LoginScreen;
  ```
  Create `HomeScreen.tsx`
  Define the home screen:
  
  ```tsx
  import React from "react";
  import { View, Text, Button, StyleSheet } from "react-native";
  import { StackNavigationProp } from "@react-navigation/stack";
  import { RootStackParamList } from "../navigation/AppNavigator";
  
  type HomeScreenNavigationProp = StackNavigationProp<RootStackParamList, "Home">;
  
  type Props = {
    navigation: HomeScreenNavigationProp;
  };
  
  const HomeScreen: React.FC<Props> = ({ navigation }) => {
    const handleLogout = () => {
      navigation.replace("Login");
    };
  
    return (
      <View style={styles.container}>
        <Text style={styles.title}>Welcome to the Home Screen!</Text>
        <Button title="Logout" onPress={handleLogout} />
      </View>
    );
  };
  
  const styles = StyleSheet.create({
    container: { flex: 1, justifyContent: "center", padding: 16 },
    title: { fontSize: 24, marginBottom: 16, textAlign: "center" },
  });
  
  export default HomeScreen;
  ```
- ## 5. Modify `App.tsx`
  Update your `App.tsx` to load the `AppNavigator`:
  
  ```tsx
  import React from "react";
  import AppNavigator from "./src/navigation/AppNavigator";
  
  const App: React.FC = () => {
    return <AppNavigator />;
  };
  
  export default App;
  ```
- ## 6. Test Your App
  Run the app:
  
  ```bash
  npx react-native run-android
  # OR
  npx react-native run-ios
  ```
  You should see the **Login Screen** first. Enter credentials, and on successful login, it should navigate to the **Home Screen**. The logout button takes you back to the login screen.
- ## Optional Enhancements
	- logseq.order-list-type:: number
	  
	  **Authentication State Management**:
	  Use `React Context` or a state management library like Redux to handle authentication state globally.
	- logseq.order-list-type:: number
	  
	  **Styling**:
	  Use libraries like `styled-components` or `tailwind-rn` to style your app beautifully.
	- logseq.order-list-type:: number
	  
	  **Form Validation**:
	  Use `react-hook-form` or `Formik` to handle form validation.