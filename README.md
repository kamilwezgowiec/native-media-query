# React Native Responsive Style

## What is React Native Responsive Style

React Native Responsive Style is a TypeScript-first responsive stylesheet compatible with React Native, React Native Web and Next.js (including SSR).

Inspired and based on [react-native-media-query](https://github.com/kasinskas/react-native-media-query), this package removes the requirement of using
a 2nd prop (dataSet) when applying styles to components. In addition, this allows us now to pass arrays of styles into components like in the [example](#usage).

## Installation

### npm

```
npm install react-native-responsive-style
```

### yarn

```
yarn add react-native-responsive-style
```

## Usage

### index.tsx

```ts
import React, { useState } from "react";
import { Pressable, Text, View } from "react-native";
import { StyleSheet } from "react-native-responsive-style";

const styles = StyleSheet.create({
  container: {
    width: "100%",
    backgroundColor: "brown",

    "@media (min-width: 400px) and (max-width: 600px)": {
      backgroundColor: "yellow",
    },
    "@media (min-width: 600px)": {
      backgroundColor: "red",
    },
  },
  anotherContainer: {
    height: 300,

    "@media (min-width: 400px) and (max-width: 600px)": {
      height: 400,
    },
    "@media (min-width: 600px)": {
      height: 500,
    },
  },
  text: {
    color: "red",

    "@media (min-width: 500px)": {
      color: "blue",
    },
  },
});

export default function App() {
  const [state, setState] = useState(true);

  return (
    <View style={[styles.container, styles.anotherContainer]}>
      <Text>Welcome to Expo + Next.js 👋</Text>

      <Pressable onPress={() => setState(!state)}>
        <Text>click me ;)</Text>
      </Pressable>

      {state && (
        <Text style={styles.text}>Hi there, I am a secret message</Text>
      )}
    </View>
  );
}
```

## SSR with Next.js

In order to have server side rendering enabled, we need to use `<StyleSheet.renderSsr />` by rendering media queries in our website's `<head>` section.

### \_document.tsx

```ts
import Document, { Html, Head, Main, NextScript } from "next/document";
import { StyleSheet } from "react-native-responsive-style";

class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          <StyleSheet.renderSsr />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}

export default MyDocument;
```