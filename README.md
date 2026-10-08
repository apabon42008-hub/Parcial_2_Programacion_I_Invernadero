Greenhouse Observation System
A Python console application that simulates an environmental monitoring system for a greenhouse. The program records temperature and relative humidity readings, validates them according to the sensor's allowed ranges, and classifies the greenhouse conditions as Critical, Optimal, or Observation. It also allows the user to manage readings through a CRUD menu (add, read, update, and delete) and stores the information in a CSV file.

Note: The program's on-screen messages and prompts are in Spanish. This README explains them in English.

Table of Contents
Features
Requirements
Installation and Usage
Sensor Ranges
Program Flow
Usage Guide
Condition Classification
Example Session
Generated CSV File
Implemented Validations
Code Structure
Known Limitations
Future Improvements
Author
Features
Temperature monitoring in Celsius.
Relative humidity monitoring in percentage.
Validation according to the greenhouse sensor ranges.
Automatic classification of each reading:
Crítico (Critical)
Óptimo (Optimal)
Observación (Observation)
Automatic recommendation of an action depending on the detected conditions.
CRUD menu for greenhouse readings:
Add
Read
Update
Delete
Maximum of 8 readings in the session.
Import of previously stored readings from invernadero.csv.
Automatic CSV update after modifications.
Final report containing:
Number of readings
Minimum temperature
Maximum temperature
Average temperature
Minimum humidity
Maximum humidity
Average humidity
Uses camelCase naming for variables.
Uses while loops for the program's main control structures.
Requirements
Python 3.6 or higher
No external libraries are required.
The program uses Python's standard-library csv module.
To check your Python version:

python --version
Installation and Usage
Clone the repository
git clone https://github.com/YOUR-USERNAME/REPOSITORY-NAME.git
cd REPOSITORY-NAME
Run the program
python main.py
The program will attempt to import existing readings from:
invernadero.csv
If the file does not exist, the program starts with an empty list of readings.

Sensor Ranges
The program uses the following ranges:

Parameter	Sensor Range	Optimal Range	Critical Range
Temperature	-10 °C to 60 °C	18 °C to 26 °C	12 °C to 32 °C
Humidity	0% to 100%	60% to 80%	40% to 90%
The sensor range determines whether the entered value is physically valid.

The critical and optimal ranges determine the greenhouse condition.

Program Flow
The general program flow is:

Start
  |
  v
Import CSV
  |
  v
Display Menu
  |
  +----> 1. Add Reading
  |          |
  |          v
  |     Validate Data
  |          |
  |          v
  |     Classify Condition
  |          |
  |          v
  |     Save to CSV
  |
  +----> 2. Read Readings
  |
  +----> 3. Update Reading
  |          |
  |          v
  |     Validate New Data
  |          |
  |          v
  |     Update Reading
  |
  +----> 4. Delete Reading
  |
  +----> 5. Generate Report
  |
  +----> 0. Exit
             |
             v
          Save CSV
             |
             v
            End
Usage Guide
After starting the program, the following menu is displayed:

1. Agregar
2. Leer
3. Actualizar
4. Borrar
5. Reporte
0. Salir
These options correspond to Add, Read, Update, Report, and Exit.

1. Add (Agregar)
Adds a new temperature and humidity reading.

The program asks for:

Temperatura:
Humedad:
The values are validated against the sensor ranges.

A maximum of 8 readings can be stored.

For example:

Temperatura: 22
Humedad: 70
The program classifies this reading as:

Óptimo
and recommends:

Condiciones óptimas
2. Read (Leer)
Displays all readings currently stored.

Example:

1 22.0 °C 70.0 % Óptimo Condiciones óptimas
2 35.0 °C 50.0 % Crítico Activar protocolo de emergencia
3. Update (Actualizar)
Allows an existing reading to be modified.

The program asks for the reading number:

Lectura:
Then it asks for the new temperature and humidity.

The condition and recommended action are recalculated using the new values.

4. Delete (Borrar)
Deletes a selected reading.

The program asks for the reading number:

Lectura:
After deletion, the remaining readings are renumbered.

5. Report (Reporte)
Generates a summary using all registered readings.

The report includes:

Total number of readings
Minimum temperature
Maximum temperature
Average temperature
Minimum humidity
Maximum humidity
Average humidity
Example:

Lecturas: 3
Temperatura: 15.0 25.0 20.0
Humedad: 55.0 75.0 65.0
0. Exit (Salir)
Ends the program.

Before exiting, all current readings are saved to:

invernadero.csv
Condition Classification
The program first checks whether the values are inside the critical ranges.

Critical
A reading is classified as Crítico when either the temperature or humidity is outside the critical range.

Temperature < 12 or Temperature > 32
OR
Humidity < 40 or Humidity > 90
The recommended action is:

Activar protocolo de emergencia
Optimal
A reading is classified as Óptimo when both values are inside their optimal ranges.

18 <= Temperature <= 26
AND
60 <= Humidity <= 80
The recommended action is:

Condiciones óptimas
Observation
If the reading is valid but is not optimal or critical, it is classified as Observación.

Depending on the value, the program recommends:

Condition	Action
Temperature > 26 °C	Ventilar
Temperature < 18 °C	Calefacción
Humidity > 80%	Deshumidificar
Humidity < 60%	Nebulizar
Within acceptable conditions	Mantener
Example Session
1. Agregar
2. Leer
3. Actualizar
4. Borrar
5. Reporte
0. Salir

Opción: 1

Temperatura: 22
Humedad: 70

1 22.0 °C 70.0 % Óptimo Condiciones óptimas
Adding another reading:

Opción: 1

Temperatura: 35
Humedad: 50

2 35.0 °C 50.0 % Crítico Activar protocolo de emergencia
Reading the stored data:

Opción: 2

1 22.0 °C 70.0 % Óptimo Condiciones óptimas
2 35.0 °C 50.0 % Crítico Activar protocolo de emergencia
Generating the report:

Opción: 5

Lecturas: 2
Temperatura: 22.0 35.0 28.5
Humedad: 50.0 70.0 60.0
Generated CSV File
The program creates:

invernadero.csv
The file contains the information of every registered reading.

Example:

lectura,temperatura,humedad,estado,accion
1,22.0,70.0,Óptimo,Condiciones óptimas
2,35.0,50.0,Crítico,Activar protocolo de emergencia
The CSV is opened in write mode, so its contents are updated to reflect the current list of readings.

The program also attempts to import this file when it starts, allowing previously stored readings to be loaded.

Implemented Validations
Validation	Behavior
Temperature below -10 °C	Invalid sensor value
Temperature above 60 °C	Invalid sensor value
Humidity below 0%	Invalid sensor value
Humidity above 100%	Invalid sensor value
Invalid numeric input	Shows an invalid-data message
More than 8 readings	New readings are not accepted
Invalid update position	Reading is not updated
Invalid delete position	Reading is not deleted
Temperature outside critical range	Reading becomes Critical
Humidity outside critical range	Reading becomes Critical
Temperature and humidity inside optimal ranges	Reading becomes Optimal
Code Structure
Element	Description
tempOptima	Optimal temperature range
tempCritica	Critical temperature range
tempSensor	Temperature sensor limits
humOptima	Optimal humidity range
humCritica	Critical humidity range
humSensor	Humidity sensor limits
lecturas	List containing greenhouse readings
temp	Current temperature
hum	Current humidity
estado	Reading classification
accion	Recommended action
opcion	Selected menu option
posicion	Reading position for update/delete
archivo	CSV file name
Program sections:

Constants and variables
CSV import
Main while menu
CRUD operations
Reading validation
Condition classification
CSV update
Final report
Suggested repository structure:

repository-name
├── main.py
├── invernadero.csv
└── README.md
Known Limitations
The program supports a maximum of 8 readings in the current session.
The greenhouse sensor ranges are hardcoded in the source code.
The optimal and critical ranges are also hardcoded.
The CSV file is overwritten when the current data is saved.
There is no timestamp associated with each reading.
The program is console-based and does not include a graphical interface.
The CSV stores the current state of the readings rather than maintaining a historical database.
The program uses while loops instead of separating the program into custom functions.
Future Improvements
Add timestamps to every greenhouse reading.
Store historical measurements instead of overwriting the CSV.
Add graphical charts for temperature and humidity.
Add a graphical user interface.
Connect the system to a real temperature and humidity sensor.
Add automatic alerts for critical conditions.
Allow the user to configure the optimal and critical ranges.
Improve validation for every numeric input.
Store the data in a database instead of a CSV file.
Add more environmental variables such as soil moisture, light intensity, and CO₂.
Author
Andrés Felipe Pabón Barbosa

GitHub: @apabon42008-hub

License
This project is distributed under the MIT License. See the LICENSE file for more information.
