# Ex06 BMI Calculator
## Date: 29/05/2025

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
# Home.js
```Home.js
import React from 'react';
import { Link } from 'react-router-dom';

function Home() {
  return (
    <div className="container">
      <h1>Welcome to the BMI Calculator</h1>
      <Link to="/bmi">
        <button>Start BMI Calculation</button>
      </Link>
    </div>
  );
}

export default Home;
```
# Result.js
```Result.js
import React from 'react';
import { useLocation, useNavigate } from 'react-router-dom';

function Result() {
  const { state } = useLocation();
  const navigate = useNavigate();

  if (!state) {
    return <p>No data provided</p>;
  }

  const heightInMeters = parseFloat(state.height) / 100;
  const weight = parseFloat(state.weight);
  const bmi = weight / (heightInMeters * heightInMeters);
  let category = '';

  if (bmi < 18.5) category = 'Underweight';
  else if (bmi < 24.9) category = 'Normal';
  else if (bmi < 29.9) category = 'Overweight';
  else category = 'Obese';

  return (
    <div className="container">
      <h2>Your BMI Result</h2>
      <p><strong>BMI:</strong> {bmi.toFixed(2)}</p>
      <p><strong>Category:</strong> {category}</p>
      <button onClick={() => navigate('/bmi')}>Calculate Again</button>
    </div>
  );
}

export default Result;
```
# BMI Calculator
```js
import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';

function BMICalculator() {
  const [height, setHeight] = useState('');
  const [weight, setWeight] = useState('');
  const [error, setError] = useState('');
  const navigate = useNavigate();

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!height || !weight || isNaN(height) || isNaN(weight)) {
      setError('Please enter valid height and weight');
      return;
    }
    setError('');
    navigate('/result', { state: { height, weight } });
  };

  return (
    <div className="container">
      <h2>BMI Calculator</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Height in cm"
          value={height}
          onChange={(e) => setHeight(e.target.value)}
        />
        <input
          type="text"
          placeholder="Weight in kg"
          value={weight}
          onChange={(e) => setWeight(e.target.value)}
        />
        <button type="submit">Calculate</button>
        {error && <p style={{ color: 'red' }}>{error}</p>}
      </form>
    </div>
  );
}

export default BMICalculator;
```
# Footer.js
```js
import React from 'react';

function Footer() {
  return (
    <footer className="footer">
      <p>© 2025 Yogesh - Reg No: 212222040185</p>
    </footer>
  );
}

export default Footer;
```
# App.js
```js
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './components/Home';
import BMICalculator from './components/BMICalculator';
import Footer from './components/Footer';
import Result from './components/Result';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/bmi" element={<BMICalculator />} />
        <Route path="/result" element={<Result />} />
      </Routes>
      <Footer/>
    </Router>
  );
}

export default App;
```


## OUTPUT
![image](https://github.com/user-attachments/assets/6e1dfd92-23a8-45e1-9351-66d8316c7162)
![image](https://github.com/user-attachments/assets/2491b0fd-04a8-4512-a3c1-b80774c196af)
![image](https://github.com/user-attachments/assets/3a180d3a-6f4f-4523-bf21-8c7843618027)




## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
