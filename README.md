# Evolving-Web
# Data Fetching and Display Component

This project demonstrates a React.js component that fetches data from an API and displays it. It includes a custom hook to handle the data fetching logic, along with proper loading and error handling.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Components](#components)
- [Custom Hook](#custom-hook)
- [Contributing](#contributing)
- [License](#license)

## Introduction
This project is a simple example of using React.js to fetch data from an API and display it in a user-friendly manner. It demonstrates the use of custom hooks, state management, and conditional rendering.

## Features
- Fetches data from a specified API
- Displays loading and error states
- Reusable custom hook for data fetching
- Conditional rendering based on the fetch status

## Installation
To get started with this project, follow these steps:

1. **Clone the repository**:
   ```sh```
   ```git clone https://github.com/your-username/data-fetching-component.git```

2. **Navigate to the project directory**:
    ```cd data-fetching-component```

3. **Install dependencies**:
    ```npm install```

## Usage
To run the project locally, use the following command:
    ```npm start```

This will start the development server and open the application in your default web browser.

## Components

**DataDisplay**

The DataDisplay component is responsible for fetching and displaying data from the API. It utilizes the custom useFetch hook to handle the data fetching logic.

**Code**:

```Javascript
import React from 'react';
import useFetch from './useFetch';

const DataDisplay = () => {
    const { data, loading, error } = useFetch('https://api.example.com/data');

    if (loading) {
        return <div>Loading...</div>;
    }

    if (error) {
        return <div>Error: {error.message}</div>;
    }

    return (
        <div>
            <h1>Fetched Data</h1>
            <ul>
                {data.map((item) => (
                    <li key={item.id}>{item.name}</li>
                ))}
            </ul>
        </div>
    );
};

export default DataDisplay;
```

## Custom Hook

**useFetch**
The useFetch hook is a custom hook that handles data fetching logic. It manages loading, error, and data states, making it reusable across different components.

**Code**:

```Javascript
import { useState, useEffect } from 'react';

const useFetch = (url) => {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        fetch(url)
            .then((response) => {
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                return response.json();
            })
            .then((data) => {
                setData(data);
                setLoading(false);
            })
            .catch((error) => {
                setError(error);
                setLoading(false);
            });
    }, [url]);

    return { data, loading, error };
};

export default useFetch;
```

## Contributing
Contributions are welcome! If you find a bug or have a suggestion for improvement, please open an issue or create a pull request.

## License
This project is licensed under the MIT License. See the LICENSE file for more information.