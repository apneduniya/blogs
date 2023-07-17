---
title: "How to solve DataGrid (MUI) issue: Cannot read properties of undefined (reading 'mode')"
seoTitle: "How to Solve DataGrid (MUI) Issue: Cannot read properties of undefined"
seoDescription: "Learn how to fix the 'Cannot read properties of undefined (reading 'mode')' error in MUI's DataGrid component. Find step-by-step solutions and code examples"
datePublished: Mon Jul 17 2023 12:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clk6td32g0th7fgnv62pbf7dd
slug: how-to-solve-datagrid-mui-issue-cannot-read-properties-of-undefined-reading-mode
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689579470414/690b7d71-e777-41a5-9b6b-ab70b6f0599b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689579992847/e2b53dc2-d498-47b6-b842-cbd666a4e032.png
tags: reactjs, mui

---

## What is MUI?

![MUI Grid System Getting Started](https://blog.logrocket.com/wp-content/uploads/2021/12/mui-grid-system-getting-started.png align="center")

[MUI](https://mui.com/) is a React library that implements Google’s Material Design and its grid system. Widely used in Android app development, MUI defines a set of principles and guidelines for designing UI components. The creators of this technology shortened the project’s name from [Material UI to MUI in September 2021](https://mui.com/blog/material-ui-is-now-mui/#:~:text=A%20new%20name,pronounced%20%2F%C9%9Bm%20ju%CB%90%20a%C9%AA%2F.), clarifying that the project was never affiliated with Google.

MUI comes with prebuilt UI components, including buttons, navbars, navigation drawers, and, most importantly, the grid system. [MUI v5 offered new features](https://mui.com/blog/mui-core-v5/), an updated design, performance optimization, and enhanced theming options.

### *Cannot read properties of undefined (reading 'mode')*

I came up with this error a few days ago and it took me a day to solve this (because I was new to MUI and ChatGPT too can't figure it out 🥺).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689577564731/220c6a57-321a-47ed-b27e-d691803da52a.png align="center")

You might come up with this error, whatever you have written all the required `props` and installed all the [required packages](https://mui.com/x/react-data-grid/getting-started/#installation):

```javascript
yarn add @mui/x-data-grid
```

The Data Grid package has a peer dependency on `@mui/material`. If you are not already using it in your project, you can install it with:

```javascript
npm install @mui/material @emotion/react @emotion/styled
```

And your code would more or less look like this...

```javascript
import * as React from 'react';
import { DataGrid, GridRowsProp, GridColDef } from '@mui/x-data-grid';

const rows: GridRowsProp = [
  { id: 1, col1: 'Hello', col2: 'World' },
  { id: 2, col1: 'DataGridPro', col2: 'is Awesome' },
  { id: 3, col1: 'MUI', col2: 'is Amazing' },
];

const columns: GridColDef[] = [
  { field: 'col1', headerName: 'Column 1', width: 150 },
  { field: 'col2', headerName: 'Column 2', width: 150 },
];

export default function App() {
  return (
    <div style={{ height: 300, width: '100%' }}>
      <DataGrid rows={rows} columns={columns} />
    </div>
  );
}
```

So you might be wondering why it is not showing like this 🤔

%[https://codesandbox.io/embed/datagrid-0whfr?fontsize=14&hidenavigation=1&theme=dark&view=preview] 

## Solution 😊

This is what worked for me... I had to add the `MuiDataGrid` object to `createTheme()`. As I was just integrating `DataGrid`, I haven't thought to add `<ThemeProvider>` of MUI 🤦.

```javascript
const MuiTheme = createTheme({
  palette: {
    mode: "dark",
  },
  components: {
    MuiDataGrid: {
      styleOverrides: {
        root: {
          border: 1,
          borderColor: colors.primaryGrayMid,
          borderStyle: "solid",
          borderRadius: 10,
          boxShadow: "0px 0px 10px rgba(0, 0, 0, 0.25)",
          backgroundColor: colors.primaryGrayDark,
          color: "#C1C2C5",
          padding: 10,
        },
      },
    },
  },
});

 <ThemeProvider theme={MuiTheme}>
     {...}
 </ThemeProvider>
```

Hope, this might save your day and if yes then please like it as it took a lot of effort to write this for you and also give your feedback on where I can improve more 🙃.