---
author: Pratik Chandlekar
pubDatetime: 2023-04-04T17:05:16Z
title: "Building Multi-page Signup Login React Native App Part 2"
postSlug: "building-multi-page-signup-login-react-native-app-part-2"
featured: false
draft: false
tags:
  - mobile-app
  - react-native
ogImage: ""
description: Learn how to create a beautiful and responsive Login and Signup UI in React Native using TailwindCSS and functional reusable components with Props. Enhance your front-end development skills with this step-by-step tutorial and improve user experience for your mobile application. Follow along and create visually appealing forms that are both easy to use and efficient.
---

## Introduction

In this second part of our multi-part series, we will continue building our multi-page signup/login app in React Native. In this blog, we will cover the following topics:

1. Styling components using TailwindCSS
1. Creating individual React Native components with the ability to pass props.

> Disclaimer: This project is UI-focused, with an emphasis on styling and design. It's a mobile app, but it's not connected to any backend or database, so all the data is hard-coded in the pages. The primary goal of this project is to practice coding and explore various design ideas, with the aim of producing a visually appealing and functional mobile app.

<!-- ## Creating individual React Native components with the ability to pass props -->

Few steps to follow before we start.

1. To keep our reusable React Native components in an organized manner, let's create a folder named `components`.
1. You can create a folder named `assets` to store images, SVGs, and other static resources that are required in your React Native app.

## Design System (colors)

We are going to use the following colors:

1. For Backgroud: #fff ie `white` in tailwindcss
1. For dark text: '#3F3D56'
1. For white text: '#f3f4f6'
1. Primary Color: '#8B5CF6' ie `blue-500` in tailwindcss
1. bgGray: '#e4e4e7'

To use colors more conveniently in Tailwind CSS classes, we can add them to the Tailwind config file:

tailwind.config.js

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./App.{js,jsx,ts,tsx}",
    "./components/*.{js,jsx,ts,tsx}",
    "./pages/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        textDark: "#3F3D56",
      },
    },
  },
  plugins: [],
};
```

To ensure that we can apply Tailwind CSS to the components that will be present inside the `components` directory, we have included this directory in the content section of the Tailwind CSS configuration file.

To style components using props, we will also use React Native Stylesheet. To define all the necessary color values, we will create a `colors.js` file in the `assets/folder`.

assets/colors.js

```javascript
export default {
  textDark: "#3F3D56",
  textWhite: "#f3f4f6",
  primary: "#8B5CF6",
  bgGray: "#e4e4e7",
};
```

## Creating Heading Component.

Creating a `Header Text` that will be visible on all the pages.

Greeting.tsx

```javascript
<Text className="text-textDark text-4xl font-extrabold">CodeGenius</Text>
```

To ensure reusability of the Heading component across all pages, it is best practice to create a separate component file for it.

Create a Heading component `components/Heading.tsx`.

```javascript
import { Text } from "react-native";
import React from "react";

export default function Heading(props) {
  return (
    <Text className="text-textDark text-4xl font-extrabold">
      {props.content}
    </Text>
  );
}
```

We will make the Heading component reusable by passing text as a prop, enabling us to use the same component for displaying headings with different text.

We will import the reusable `Heading` component in `pages/Greeting.tsx` and pass the content prop to it, as shown below:

```javascript
import Heading from "../components/Heading";

const Greeting = ({ navigation }) => {
  return (
    <SafeAreaView className="bg-white container h-full px-7">
      <Heading content="CodeGenius" />

      <View className="mt-6">
        <TouchableOpacity
          className="mt-3 rounded-xl py-3"
          style={{ elevation: 1, backgroundColor: colors.primary }}
          onPress={() => navigation.navigate("Login")}
        >
          <Text
            className="text-center text-base"
            style={{ color: colors.textWhite }}
          >
            Login
          </Text>
        </TouchableOpacity>
        <CustomButton
          navigation={navigation}
          bgColor={colors.bgGray}
          textColor={colors.textDark}
          goto={"Signup"}
          content={"Singup"}
        />
      </View>
    </SafeAreaView>
  );
};
```

This is how our application looks now:

<p align = "center">
<img src = "/assets/06-building-multi-page-signup-login-react-native-app-part-2/heading.png">
</p>
<p align = "center">
Fig. 1 - Heading Component
</p>

## Hero image

If you want to add a vector art to your greeting page, you'll need to write some code. While there are plenty of image and vector art resources available online, we'll be using an image from [undraw](https://undraw.co/illustrations) for this demonstration. First, download the image and save it in the assets folder of your project. Then, follow these steps to add the vector art to your project.

`pages/Greeting.tsx`

```javascript
      <View className="flex justify-center items-center mt-24">
        <Image
          source={require('./../assets/hero.png')}
          style={{width: 400, height: 300}}
        />
      </View>
      <Heading content="CodeGenius" />
```

<p align = "center">
<img src = "/assets/06-building-multi-page-signup-login-react-native-app-part-2/hero.png">
</p>
<p align = "center">
Fig. 2 - Hero Component
</p>

## Buttons

Writing code for resusable button component.
The CustomButton component in our code has been designed to be reusable in different ways. We can customize the button's appearance and functionality by passing values to different props. For example, we can use the "navigation" prop to navigate to a different page, set the background color with "bgColor" prop, set the text color with "textColor" prop, set the text content with "content" prop, and set the navigation destination with "goto" prop. By using these different props in different combinations, we can create a CustomButton component that meets our specific requirements. This allows us to create buttons quickly and efficiently for various parts of our application without having to write new code each time.

`compnents/CustomButton.tsx`

```javascript
import { TouchableOpacity, Text } from "react-native";
import React from "react";

const CustomButton = props => {
  return (
    <TouchableOpacity
      className="mt-3 rounded-xl py-3"
      style={{ elevation: 1, backgroundColor: props.bgColor }}
      onPress={() => props.navigation.navigate(props.goto)}
    >
      <Text
        className="text-center text-base"
        style={{ color: props.textColor }}
      >
        {props.content}
      </Text>
    </TouchableOpacity>
  );
};

export default CustomButton;
```

With the reusable CustomButton component we have created, we can create multiple buttons with different colors and text using props. By passing different values to the bgColor and textColor props, we can create buttons with different color schemes. Additionally, we can change the text displayed on the button by passing the desired text to the content prop. We can also use the goto prop to specify the page that the button should navigate to when it is clicked. By utilizing these props in different combinations, we can create custom buttons according to our needs.

```javascript
<CustomButton
  navigation={navigation}
  bgColor={'#f87171'}
  textColor={'#fff'}
  goto={'Signup'}
  content={'Hello'}
/>
<CustomButton
  navigation={navigation}
  bgColor={'#059669'}
  textColor={'#fff'}
  goto={'Signup'}
  content={'Click Here'}
/>
<CustomButton
  navigation={navigation}
  bgColor={colors.primary}
  textColor={colors.textWhite}
  goto={'Login'}
  content={'Login'}
/>
<CustomButton
  navigation={navigation}
  bgColor={colors.bgGray}
  textColor={colors.textDark}
  goto={'Signup'}
  content={'Singup'}
/>
```

<p align = "center">
<img src = "/assets/06-building-multi-page-signup-login-react-native-app-part-2/multiplebuttons.png">
</p>
<p align = "center">
Fig. 3 - Buttons
</p>

## Form elements

In this section, we will be styling a form that includes the following elements:

1. Text inputs for entering first name, last name, email, and password.
1. A signup button to create a new account.
1. Google and Facebook buttons to login with those accounts.
1. A link to the login page for users who already have an account.

The form will provide a simple and user-friendly way for users to sign up for our service and log in using their preferred method. By incorporating popular social media platforms, we can make the process more convenient for users and potentially attract more users to our platform. The text inputs will allow users to provide their basic information securely, and the signup button will complete the registration process. If users already have an account, they can easily access it through the login page linked in the form.

### Text inputs

Creating a text input for First Name. We will use `useState` hook which is a built-in hook in React/Reat-Native that allows functional components to have state variables and update them. It takes an initial value and returns an array with two elements: the current state value and a function to update it. This means that you can update the data within your component and React will automatically re-render the component to reflect the changes.

`pages/Signup.tsx`

```javascript
const [firstName, setFirstName] = useState("");
```

The [TextInput](https://reactnative.dev/docs/textinput) component is used to take input from keyboard in react native.

```javascript
<TextInput
  onChangeText={setFirstName}
  placeholder={"First Name"}
  placeholderTextColor={colors.textDark}
  value={firstName}
  className="bg-zinc-200 text-textgray rounded-xl py-3 px-5"
/>
```

When the user types something into the input field, the `setFirstName` function is called with the new value as an argument, and the `firstName` state variable is updated with that value. The `placeholder` prop sets the initial text displayed in the input field, while the `value` prop sets the current value of the input field. The `className` prop sets the CSS classes used for styling the input field, in this case a light gray background, dark text, and rounded corners.

In the same way we can create multiple text inputs like Last Name, Email and password.

### Social buttons

Creating a functional component called "SocialIcons" that displays two TouchableOpacity buttons with Google and Facebook logos as images.

`components/SocialIcons.tsx`

```javascript
import { View, TouchableOpacity, Image } from "react-native";
import React from "react";

const SocialIcons = () => {
  return (
    <View className="flex flex-row items-center justify-center">
      <TouchableOpacity className="bg-zinc-200 mx-2 rounded-lg px-16 py-2">
        <Image
          source={require("./../assets/google.png")}
          style={{ width: 30, height: 30 }}
        />
      </TouchableOpacity>
      <TouchableOpacity className="bg-zinc-200 mx-2 rounded-lg px-16 py-2">
        <Image
          source={require("./../assets/facebook.png")}
          style={{ width: 30, height: 30 }}
        />
      </TouchableOpacity>
    </View>
  );
};

export default SocialIcons;
```

### Complete Signup Page Code

`pages/Signup.tsx`

```javascript
import { View, Text, TouchableOpacity, TextInput } from "react-native";
import { useState } from "react";
import { SafeAreaView } from "react-native-safe-area-context";
import Heading from "../components/Heading";
import CustomButton from "../components/CustomButton";
import colors from "../assets/colors";
import SocialIcons from "../components/SocialIcons";

const Signup = ({ navigation }) => {
  const [firstName, setFirstName] = useState("");
  const [lastName, setLastName] = useState("");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  return (
    <SafeAreaView className="bg-white container h-full px-7">
      <View className="mt-24">
        <Heading content="Create Account" />
      </View>
      <View className="mt-4">
        <TextInput
          onChangeText={setFirstName}
          placeholder={"First Name"}
          placeholderTextColor={colors.textDark}
          value={firstName}
          className="bg-zinc-200 text-textgray rounded-xl py-3 px-5"
        />
        <TextInput
          onChangeText={setLastName}
          placeholder={"Last Name"}
          placeholderTextColor={colors.textDark}
          value={lastName}
          className="bg-zinc-200 text-textgray mt-3 rounded-xl py-3 px-5"
          // style={{color: '#000000'}}
        />
        <TextInput
          onChangeText={setEmail}
          placeholder={"Email"}
          placeholderTextColor={colors.textDark}
          value={email}
          className="bg-zinc-200 text-textgray mt-3 rounded-xl py-3 px-5"
        />
        <TextInput
          secureTextEntry={true}
          onChangeText={setPassword}
          placeholder={"Password"}
          placeholderTextColor={colors.textDark}
          value={password}
          className="bg-zinc-200 text-textgray mt-3 rounded-xl py-3 px-5"
        />
        <TouchableOpacity
          className="mt-2 flex items-end"
          onPress={() => navigation.goBack()}
        >
          <Text className="text-textgray font-bold">Forgot Password?</Text>
        </TouchableOpacity>
      </View>
      <CustomButton
        navigation={navigation}
        bgColor={colors.primary}
        textColor={colors.textWhite}
        goto={"Items"}
        content={"Signup"}
      />
      <View className="mt-10">
        <Text className="text-textgray text-center">Or Continue With</Text>
        <View className="mt-2">
          <SocialIcons />
        </View>
        <View className="mt-24 flex flex-row items-center justify-center">
          <Text className="text-textgray">Already have a accout?</Text>
          <TouchableOpacity onPress={() => navigation.navigate("Login")}>
            <Text className="text-textgray underline">Login</Text>
          </TouchableOpacity>
        </View>
      </View>
    </SafeAreaView>
  );
};

export default Signup;
```

<p align = "center">
<img src = "/assets/06-building-multi-page-signup-login-react-native-app-part-2/signup.png">
</p>
<p align = "center">
Fig. 4 - Signup Page
</p>

## Login Page

Similary create Login page

`pages/Login.tsx`

```javascript
import { View, Text, TouchableOpacity, TextInput, Image } from "react-native";
import { useState } from "react";
import { SafeAreaView } from "react-native-safe-area-context";
import Heading from "../components/Heading";
import CustomButton from "../components/CustomButton";
import colors from "../assets/colors";
import SocialIcons from "../components/SocialIcons";

const Login = ({ navigation }) => {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  return (
    <SafeAreaView className="bg-white container h-full px-7">
      <View className="mt-36">
        <Heading content="Welcome Back" />
      </View>
      <View className="mt-4">
        <TextInput
          onChangeText={setEmail}
          placeholder={"Email"}
          placeholderTextColor={colors.textDark}
          value={email}
          className="bg-zinc-200 rounded-xl py-3 pl-5"
        />
        <TextInput
          secureTextEntry={true}
          onChangeText={setPassword}
          placeholder={"Password"}
          placeholderTextColor={colors.textDark}
          value={password}
          className="bg-zinc-200 mt-3 rounded-xl py-3 pl-5"
        />
        <TouchableOpacity
          className="mt-2 flex items-end"
          onPress={() => navigation.goBack()}
        >
          <Text className="text-textDark font-bold">Forgot Password?</Text>
        </TouchableOpacity>
      </View>
      <CustomButton
        navigation={navigation}
        bgColor={colors.primary}
        textColor={colors.textWhite}
        goto={"Items"}
        content={"Login"}
      />
      <View className="mt-10">
        <Text className="text-textDark text-center">Or Continue With</Text>
        <View className="mt-2">
          <SocialIcons />
        </View>
        <View className="mt-44 flex flex-row items-center justify-center">
          <Text className="text-textDark">Does'nt have a accout?</Text>
          <TouchableOpacity onPress={() => navigation.navigate("Signup")}>
            <Text className="text-textDark underline">Signup</Text>
          </TouchableOpacity>
        </View>
      </View>
    </SafeAreaView>
  );
};

export default Login;
```

<p align = "center">
<img src = "/assets/06-building-multi-page-signup-login-react-native-app-part-2/login.png">
</p>
<p align = "center">
Fig. 5 - Login Page
</p>

## Conclusion

In conclusion, building a UI for a login and signup form in React Native using TailwindCSS and functional reusable components can help streamline the development process and improve the overall user experience. By leveraging the power of React Native and the flexibility of TailwindCSS, we can create stunning UIs with minimal effort, while also maintaining a high degree of customization and flexibility. Additionally, the use of functional reusable components allows developers to create modular, reusable code that can be easily scaled and adapted for future projects. Overall, the process of building a login and signup form UI in React Native with TailwindCSS is a powerful and efficient way to create sleek and user-friendly interfaces for any mobile app.
