# Tramp.Os Project Documentation

## Introduction

Welcome to the official documentation of the Tramp.Os project, a mobile application developed in React Native with Expo. This project was undertaken as part of studies in a college course and utilizes the Jsearch API from RapidAPI to search for job opportunities and display them in the application.

### Project Structure
___

The project is structured as follows:
(major folder structure)

```plaintext
Tramp.Os/
|-- app/
|   |-- jobdetails/
|   |-- search/
|   |-- _layout.js
|   |-- home.js
|   |-- index.js
|-- assets/
|   |-- fonts/
|   |-- icons/
|   |-- images/
|-- components/
|   |-- common/
|	|   |-- cards/
|	|   |-- header/
|   |-- home/
|	|   |-- nearby/
|	|   |-- popular/
|	|   |-- welcome/
|   |-- jobdetails/
|	|   |-- about/
|	|   |-- company/
|	|   |-- footer/
|	|   |-- specifics/
|	|   |-- tabs/
|   |-- index.js
|-- constants/
|   |-- icons.js
|   |-- images.js
|   |-- index.js
|   |-- theme.js
|   hook/
|   |-- useFetch.js
|-- styles/
|   |-- search.js
|-- utils/
|   |-- index.js
|-- package.json
|-- ...
```

- The `/components/` folder contains reusable components.

- The `hooks/` folder contains the `useFetch` file, responsible for making calls to the Jsearch API using Axios.

## Environment Setup
___

Ensure that Node.js, Expo CLI, and Yarn (or npm) are installed in your development environment. If not, follow the instructions in the official [Expo documentation](https://docs.expo.dev/get-started/installation/).

```bash
# Install Expo CLI globally
npm install -g expo-cli

# Install project dependencies
npm install
```

## Project Dependencies
_____

Tramp.Os uses several essential dependencies for development and proper application functioning. Below are the main dependencies, along with a brief explanation of each:

### [Expo](https://docs.expo.dev/)

Expo is a platform that facilitates the development of React Native applications by providing additional tools and services. It simplifies tasks such as accessing native device resources, making multi-platform development easier.

```bash
# Expo CLI installation
npm install -g expo-cli
```

### [React Native](https://reactnative.dev/)

React Native is a framework for building mobile applications using React and JavaScript. It enables the development of native iOS and Android apps with a common codebase.

```bash
# React Native installation
npm install react-native
```

### [Axios](https://axios-http.com/)

Axios is a Promise-based HTTP client used for making HTTP requests. It simplifies the process of communicating with APIs, providing an easy-to-use interface for making requests and handling responses.

```bash
# Axios installation
npm install axios
```

### [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

JavaScript is the programming language used to develop logic and dynamic interaction in Tramp.Os. It is the primary programming language for web and mobile development, providing the ability to create interactive and responsive applications.

No separate installation of JavaScript is required, as it is interpreted by browsers or the Node.js environment.

## Jsearch API Configuration
_____

The project uses the Jsearch API from RapidAPI to search for job opportunities. To configure the API, follow these steps:

1. Access [RapidAPI](https://rapidapi.com/).
2. Create an account or log in if you already have one.
3. Subscribe to the free plan of the Jsearch API.
4. Get the Jsearch API key on the RapidAPI settings page.
5. Replace the API key in the `hook/useFetch.js` file.

```javascript
// src/services/api.js

import { useState, useEffect } from "react";
import axios from "axios";

const useFetch = (endpoint, query) => {
  const [data, setData] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);
  
  const options = {
    method: "GET",
    url: `https://jsearch.p.rapidapi.com/${endpoint}`,
    headers: {
      "X-RapidAPI-Key": 'YOUR_API_KEY',
      "X-RapidAPI-Host": "jsearch.p.rapidapi.com",
    },
    params: { ...query },
  };

  
  const fetchData = async () => {
    setIsLoading(true);
    try {
      const response = await axios.request(options);
  
      setData(response.data.data);
      setIsLoading(false);
    } catch (error) {
      setError(error);
      console.log(error)
    } finally {
      setIsLoading(false);
    }
  };

  
  useEffect(() => {
    fetchData();
  }, []);

  const refetch = () => {
    setIsLoading(true);
    fetchData();
  };

  return { data, isLoading, error, refetch };
};
  

export default useFetch;
```

## Running the Project
_____

With the dependencies installed and the API key configured, you can start the project with the following command:

```bash
npx expo start
```

This will open the Expo Developer Tools in your browser. You can then run the app on an emulator or on a physical device using the Expo Go app.

## Notes

This project was developed based on a tutorial and as part of an academic project. If you encounter difficulties or want to contribute, feel free to open an issue or submit a pull request on the GitHub repository.

Project GitHub: [Tramp.Os](https://github.com/Yan-pi/Tramp.Os)

---

We hope this documentation is helpful for understanding the structure and setting up the environment for the Tramp.Os project. If you have additional questions, refer to the official [Expo](https://docs.expo.dev/) and [React Native](https://reactnative.dev/docs/getting-started) documentation.
