## Implementation of fuzzy logic for crop yield prediction:
This documentation provides a detailed guide on implementing a fuzzy logic system for predicting crop yield based on input variables: rainfall, temperature, and soil fertility. The implementation is done using Python and the scikit-fuzzy library.
### Prerequisites
Python (version 3.6 or later)
Virtual environment tool (optional but recommended)
### Setup Process
Install Python: Ensure Python is installed on your system. You can download it from python.org.

### Install Required Libraries:
      pip install numpy scikit-fuzzy

### Implementation
Step 1: Import Libraries
First, import the necessary libraries:

      import numpy as np
      import skfuzzy as fuzz
      from skfuzzy import control as ctrl
      
Step 2: Define Input and Output Variables
Define the input variables (rainfall, temperature, and soil_fertility) and the output variable (crop_yield):

      rainfall = ctrl.Antecedent(np.arange(0, 201, 1), 'rainfall')
      temperature = ctrl.Antecedent(np.arange(0, 51, 1), 'temperature')
      soil_fertility = ctrl.Antecedent(np.arange(0, 101, 1), 'soil_fertility')
      rop_yield = ctrl.Consequent(np.arange(0, 101, 1), 'crop_yield')

Step 3: Define Membership Functions
Define the fuzzy membership functions for each variable:

      rainfall['low'] = fuzz.trimf(rainfall.universe, [0, 0, 100])
      rainfall['medium'] = fuzz.trimf(rainfall.universe, [50, 100, 150])
      rainfall['high'] = fuzz.trimf(rainfall.universe, [100, 200, 200])

      temperature['low'] = fuzz.trimf(temperature.universe, [0, 0, 25])
      temperature['medium'] = fuzz.trimf(temperature.universe, [15, 25, 35])
      temperature['high'] = fuzz.trimf(temperature.universe, [25, 50, 50])

      soil_fertility['poor'] = fuzz.trimf(soil_fertility.universe, [0, 0, 50])
      soil_fertility['average'] = fuzz.trimf(soil_fertility.universe, [25, 50, 75])
      soil_fertility['rich'] = fuzz.trimf(soil_fertility.universe, [50, 100, 100])

      crop_yield['low'] = fuzz.trimf(crop_yield.universe, [0, 0, 50])
      crop_yield['medium'] = fuzz.trimf(crop_yield.universe, [25, 50, 75])
      crop_yield['high'] = fuzz.trimf(crop_yield.universe, [50, 100, 100])

Step 4: Define Fuzzy Rules
Create the fuzzy rules to describe how the input variables interact to influence the output variable:

      rule1 = ctrl.Rule(rainfall['low'] & temperature['medium'] & soil_fertility['poor'], crop_yield['low'])
      rule2 = ctrl.Rule(rainfall['medium'] & temperature['low'] & soil_fertility['average'], crop_yield['medium'])
      rule3 = ctrl.Rule(rainfall['high'] & temperature['high'] & soil_fertility['rich'], crop_yield['high'])
      rule4 = ctrl.Rule(rainfall['high'] & temperature['medium'] & soil_fertility['average'], crop_yield['medium'])
      rule5 = ctrl.Rule(rainfall['low'] & temperature['high'] & soil_fertility['rich'], crop_yield['low'])
      rule6 = ctrl.Rule(rainfall['low'] & temperature['low'] & soil_fertility['poor'], crop_yield['low']) 
      rule7 = ctrl.Rule(rainfall['low'] & temperature['low'] & soil_fertility['average'], crop_yield['low']) 
      rule8 = ctrl.Rule(rainfall['low'] & temperature['low'] & soil_fertility['rich'], crop_yield['medium'])
      rule9 = ctrl.Rule(rainfall['medium'] & temperature['medium'] & soil_fertility['poor'], crop_yield['medium'])
      rule10 = ctrl.Rule(rainfall['medium'] & temperature['medium'] & soil_fertility['average'], crop_yield['medium'])


Step 5: Create and Simulate the Control System
Create the control system and simulate the result:

        # Create the control system
        crop_yield_ctrl = ctrl.ControlSystem(rules)
        
        # Create a simulation
        crop_yield_simulation = ctrl.ControlSystemSimulation(crop_yield_ctrl)
        
        # Input values for prediction
        crop_yield_simulation.input['rainfall'] = 120
        crop_yield_simulation.input['temperature'] = 30
        crop_yield_simulation.input['soil_fertility'] = 70
        
        # Compute the result
        crop_yield_simulation.compute()
        
        # Output the result
        print(f"Predicted Crop Yield: {crop_yield_simulation.output['crop_yield']}")

  Step 6: Visualize the Result
Visualize the result using the built-in visualization tool:

        crop_yield.view(sim=crop_yield_simulation)
        
Running the Implementation
To run the implementation, save the code in a Python script file (e.g., crop_yield_prediction.py) and execute it in your virtual environment:

        python crop_yield_prediction.py
        
This will compute and print the predicted crop yield based on the input values and display the visualization of the fuzzy logic system.

### Conclusion:
This guide provides a step-by-step implementation of a fuzzy logic system for crop yield prediction using the scikit-fuzzy library in Python. By following the setup process and implementation steps, we can predict crop yield based on various environmental factors and visualize the results.


      



