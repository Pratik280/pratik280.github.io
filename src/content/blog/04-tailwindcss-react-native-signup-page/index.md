---
author: Pratik Chandlekar
pubDatetime: 2023-03-29T17:05:16Z
title: "Styling React Native with TailwindCSS and Navigating Between Pages with React Navigation"
postSlug: "styling-react-native-with-tailwindCSS-and-navigating-between-pages-with-react-navigator"
featured: false
draft: true
tags:
  - mobile-app
ogImage: ""
description: Tailwindcss react native
---

## Introduction

In this article, we will explore how to enhance the styling of React Native apps by using tailwindcss and nativewind. Additionally, we will cover how to navigate between multiple pages in a React Native app using React Navigation. By the end of this article, you will have learned how to:

1. Effectively incorporate tailwindcss to style React Native components.
1. Style a TouchableOpacity button using tailwindcss.
1. Implement page navigation for multiple pages, such as a Greeting page, Login page, and Sign up page, using React Navigation.

### Prerequisites

- Bare bones react native application.
- Text Editor / IDE (VS Code, Android Studio).
- Android device or Android Virtual Device for testing.

> If this is your first time working with react native, I have made a in-depth guide on [setting up development environment for react native on linux](https://pratik280.hashnode.dev/linux-devs-rejoice-a-comprehensive-guide-to-setting-up-your-react-native-development-environment).

## Setting up [Tailwindcss](https://tailwindcss.com/) with [Nativewind](https://www.nativewind.dev/) in react native application

- Tailwindcss is a css library used for web, where we style UI using pre-defined in-line css classes. It as very good default set out of the box.
- Nativewind allows us to use tailwindcss in react-native. It acts as a compatibility layer between React Native and CSS.

Creating a react native project using react-native cli:

```bash
npx react-native init tailwindSignUpForm
```

Installing node js dependencies for tailwindcss and nativewind according to [official Nativewind docs](https://www.nativewind.dev/quick-starts/react-native-cli):

```bash
npm i nativewind
npm i -D tailwindcss
```

Generate a tailwind config file using command:

```bash
npx tailwindcss init
```

This will generate a `tailwind.config.js` in the root directory of your project, simply run the command mentioned. After generating the file, you can edit its content to include the pages directory which we will create later on in the project.

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./App.{js,jsx,ts,tsx}", "./pages/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

Make the below mentioned changes in `babel.config.js`:

```javascript
module.exports = {
  presets: ["module:metro-react-native-babel-preset"],
  plugins: ["nativewind/babel"],
};
```

Replace all content in `App.tsx` with following:

```javascript
import { View, Text } from "react-native";
import React from "react";
import "nativewind/types.d";

const App = () => {
  return (
    <View className="mt-12">
      <Text className="pl-4 text-3xl font-bold">App</Text>
    </View>
  );
};

export default App;
```

Now run the app:

```
npm run android
```

```
npx react-native start
```

![App component after applying tailwind classes](/assets/04-tailwindSignup/app.png)

By applying inline Tailwind CSS classes to our app component, we have successfully styled it. You can now see the visual changes in the app.

---

## Working with React Navigation.

### What is React Navigation.

[React native official docs](https://reactnative.dev/docs/navigation#react-navigation)
[React Navigation Docs](https://reactnavigation.org/)

- React Navigation Native Stack allows us to navigate between different pages and by default it has gestures and animations are in android or ios. We wrap all navigators with NavigationContainer component.

- NavigationContainer is component that is responsible for managing the navigation tree and holds the navigation state.

- createNativeStackNavigator is a React function that returns an object with two components: Screen and Navigator.

- Screen will be our individual pages and we will house Navigator with all our individual pages that we want to navigate.

First make a pages folder. Here we will keep all our pages(Greeting page, login page and signup page)

### Setting up React Navigation in our projects.

Install

```bash
npm install @react-navigation/native @react-navigation/native-stack
```

for bare react native project

```bash
npm install react-native-screens react-native-safe-area-context
```

for expo

```bash
npx expo install react-native-screens react-native-safe-area-context
```

### Adding three pages for navigation.

import the necessary

```javascript
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
```

For time being write a simple Greeting Page
pages/Greeting.tsx

```javascript
import { View, Text } from "react-native";
import React from "react";
import { SafeAreaView } from "react-native-safe-area-context";

const Greeting = () => {
  return (
    <SafeAreaView>
      <Text>Greeting</Text>
    </SafeAreaView>
  );
};

export default Greeting;
```

> SafeAreaView for notch [Read more about SafeAreaView](https://reactnative.dev/docs/safeareaview)

Make the following changes in App.tsx

```javascript
const Stack = createNativeStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Greeting" component={Greeting} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};
```

In out navigator, we have added our Greeting component as a Screen.

![Greeting](/assets/04-tailwindSignup/greeting.png)

Add two more components Signup.tsx and Login.tsx

components/Signup.tsx

```javascript
import { View, Text } from "react-native";
import React from "react";
import { SafeAreaView } from "react-native-safe-area-context";

const Signup = () => {
  return (
    <SafeAreaView>
      <Text>Signup</Text>
    </SafeAreaView>
  );
};

export default Signup;
```

components/Login.tsx

```javascript
import { View, Text } from "react-native";
import React from "react";
import { SafeAreaView } from "react-native-safe-area-context";

const Login = () => {
  return (
    <SafeAreaView>
      <Text>Login</Text>
    </SafeAreaView>
  );
};

export default Login;
```

Add newly created components in Navigator in App.tsx

```javascript
import { View, Text } from "react-native";
import React from "react";
import "nativewind/types.d";
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import Signup from "./components/Signup";
import Login from "./components/Login";
import Greeting from "./components/Greeting";

const Stack = createNativeStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Greeting" component={Greeting} />
        <Stack.Screen name="Signup" component={Signup} />
        <Stack.Screen name="Login" component={Login} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
```

Now in Greeting component we will add Links(buttons) to navigate to other components ie Login Page and Signup Page

```javascript
import { View, Text, TouchableOpacity } from "react-native";
import React from "react";
import { SafeAreaView } from "react-native-safe-area-context";

const Greeting = ({ navigation }) => {
  return (
    <SafeAreaView>
      <Text>Greeting</Text>
      <TouchableOpacity onPress={() => navigation.navigate("Signup")}>
        <Text>Signup</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={() => navigation.navigate("Login")}>
        <Text>Login</Text>
      </TouchableOpacity>
    </SafeAreaView>
  );
};

export default Greeting;
```

- Because of navigation.navigate("Signup"), when we click on Singup button it will navigate to Signup page. And the title on Signup page will have a back button as well that will bring us back on Greeting page.

- Similarly, navigation.navigate("Login") will navigate to Login page.

![Greeting](/assets/04-tailwindSignup/navigator-work.png)
![Greeting](/assets/04-tailwindSignup/navigator-work-2.png)

## Adding back button

Now we will add back button on Login page that will redirect us back to Greeting page.

```javascript
import { View, Text, TouchableOpacity } from "react-native";
import React from "react";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";

const Login = ({ navigation }) => {
  return (
    <SafeAreaView>
      <Text>Login</Text>
      <TouchableOpacity onPress={() => navigation.goBack()}>
        <Text>Back</Text>
      </TouchableOpacity>
    </SafeAreaView>
  );
};

export default Login;
```

- onPress={() => navigation.goBack()} will take us back to Greeting page.

- The Navigator component is organized as a stack where each page is stacked on top of the previous one as we navigate through the app. Using the goBack() method, we can remove the topmost page from the stack and return to the previously active page.

### Working with button using tailwindcss and customizing Navigation Header

#### Styling Button using Tailwindcss.

Applying some styles to buttons

```javascript
<TouchableOpacity
  className="bg-indigo-500 mr-3 mt-2 rounded-md py-2"
  style={{ elevation: 3 }}
  onPress={() => navigation.navigate("Signup")}
>
  <Text className="text-gray-100 text-center text-base">Signup</Text>
</TouchableOpacity>
```

#### Customization of Navigation Header

We can customize header by passing more options

```javascript
const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Greeting"
          component={Greeting}
          options={{
            title: "Home",
            headerStyle: {
              backgroundColor: "#6366f1",
            },
            headerTintColor: "#fff",
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
};
```

![Greeting](/assets/04-tailwindSignup/color-buttons.png)

Additionally, we can also hide the header of navbar by passing a prop `headerShown:false` to screen

```javascript
const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Greeting"
          component={Greeting}
          options={{ headerShown: false }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
};
```

![Greeting](/assets/04-tailwindSignup/no-header.png)

[More on customizing Header](https://reactnavigation.org/docs/headers)

## Conclusion

<!-- ## SignUp form

folder assets, pages, components

Install for svg

```bash
npm install --save react-native-svg
``` -->
