# InternshipTask
Single Page Application using React, that involves parsing data from the api

The task is to Develop a simple one-page react application to fetch and display data from the API given below
in the form of a table.
Display a table with the following fields: City State, Country, Postcode, Street Number, Name,
Latitude, Longitude by parsing data from this API endpoint: https://randomuser.me/api/?results=20

Step 1: Create react app, prerequisite already installed nodejs and npm
Step 2: Install Axios
Step 3: In project folder, created a DataTable.js with the following code:
 import React, { useState, useEffect } from 'react';
import axios from 'axios';

const DataTable = () => {
  const [data, setData] = useState([]);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get('https://randomuser.me/api/?results=20');
        setData(response.data.results);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    fetchData();
  }, []);

  return (
    <div>
      <h2>User Data Table</h2>
      <table>
        <thead>
          <tr>
            <th>City State</th>
            <th>Country</th>
            <th>Postcode</th>
            <th>Street Number</th>
            <th>Name</th>
            <th>Latitude</th>
            <th>Longitude</th>
          </tr>
        </thead>
        <tbody>
          {data.map((user, index) => (
            <tr key={index}>
              <td>{`${user.location.city}, ${user.location.state}`}</td>
              <td>{user.location.country}</td>
              <td>{user.location.postcode}</td>
              <td>{user.location.street.number}</td>
              <td>{`${user.name.first} ${user.name.last}`}</td>
              <td>{user.location.coordinates.latitude}</td>
              <td>{user.location.coordinates.longitude}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default DataTable;

Step 4: Use the DataTable component in src/App.js:
Open src/App.js and modify it to use the DataTable component:

import React from 'react';
import './App.css';
import DataTable from './DataTable';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <DataTable />
      </header>
    </div>
  );
}

export default App;

Step 5: Run the app


