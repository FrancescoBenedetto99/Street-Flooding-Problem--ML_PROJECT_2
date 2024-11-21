# Street Flooding Simulation

Project for the Machine Learning course held at @Politecnico di Milano.

---

## INTRODUCTION

This project aims to develop a machine learning model capable of predicting flood event outcomes based on street initial conditions. A dataset of 3,000 simulated flood incidents (training set) serves as historical data points to train the model.

The goal of this project is to build a data-driven model that captures the underlying logic of the simulator generating these incidents and can replicate its predictions. Each simulated incident is unique, beginning with distinct initial conditions and leading to different outcomes. However, the geographical layout, including the street network and location coordinates of each street segment, remains unchanged across simulations. This consistent geographic information is available in the `edge_info.csv` file.

Additionally, specific parameters influencing flood progression in each simulation are defined at the start and vary across incidents. These parameters are detailed in the `training_parameters.csv` and `test_parameters.csv` files for the training and testing datasets, respectively.

### Basic Definitions

- **Nodes**: Represent intersections or endpoints of streets. Each node has a unique 9-digit identifier, such as 152356047.
- **Edges**: Street segments connecting two nodes, defined by 'head_id' and 'tail_id'.

<div align="center">
   <img width="418" alt="Screenshot 2024-11-06 alle 13 47 39" src="https://github.com/user-attachments/assets/dd59a7d8-26c3-48e4-a9cd-8b4eb4000bbb">
   <br>
   <strong><em>Figure 1 – Four street segments (edges)</em></strong>
</div>

<br> <!-- Spazio extra tra figura e testo -->

Figure 1 shows an isolated block composed of 4 street segments. The cyan-colored edge (on the left) can be represented by its head and tail nodes: 152356050 and 152356047.

The selected urban area consists of 191 edges, illustrated in Figure 2.

<div align="center">
   <img width="240" alt="Screenshot 2024-11-06 alle 13 49 24" src="https://github.com/user-attachments/assets/0e57f8a6-d8a8-4051-ba55-0e2f8b761630">
   <br>
   <strong><em>Figure 2 – The edges of the urban area</em></strong>
</div>

<br> <!-- Spazio extra tra figura e testo -->

---

## DATASET OVERVIEW

The dataset contains 3,000 observations, each detailing the initial and final states of separate flood events. These observations represent flood progression in a hypothetical urban layout defined by factors such as street connectivity, elevation, and infrastructure.

- **`./training`**
- **`./training_parameters.csv`**

<div align="center">
   <img width="856" alt="Screenshot 2024-11-06 alle 13 53 53" src="https://github.com/user-attachments/assets/1d925312-da00-44e9-a22e-646eb0a84711">
   <br>
   <strong><em>Figure 3 – Initial and final states of each observation in the ‘training’ folder</em></strong>
</div>

<br> <!-- Spazio extra tra figura e testo -->

Each CSV file in the `training` folder represents one observation's initial and final states, with file names corresponding to the `ObservationIndex` column in `training_parameters.csv`.

### Simulation Parameters

Simulation parameters for each observation are in `./training_parameters.csv` and `./test_parameters.csv`:

- **ObservationIndex**: Unique identifier for the observation.
- **SurfaceType**: Type of urban surface.
- **Waterflow** (recorded as RainfallIntensity in the CSV file): Intensity and duration of water flow.
- **InitialWaterLevels** (recorded as Init_Max_hour in the CSV file): Underground water level before the simulation.
- **DrainageSystemCapacity**: Indicator of drainage efficiency.
- **GreenSpaceRatio**: Proportion of greenery in the urban area.

These parameters represent averages across the urban area; microscopic values per edge/street are not available.

### Observation Files

The `./training` and `./test` directories contain CSV files corresponding to each observation. Each file, named after the observation index, records attributes for various edges:

- **head_id**: ID of the head node.
- **tail_id**: ID of the tail node.
- **flooded_init**: Indicates whether the edge was initially flooded.
- **flooded_final**: Indicates whether the edge was flooded at the end of the simulation (this is the target variable for prediction).

Additional information on edges is in `edge_info.csv`, including:

- **longitude**: Longitude of the edge's center.
- **latitude**: Latitude of the edge's center.
- **altitude**: Elevation of the edge's center.

<div align="center">
   <img width="866" alt="Screenshot 2024-11-06 alle 13 55 06" src="https://github.com/user-attachments/assets/00d5856d-8172-4e7a-8535-07fe052eec0f">
   <br>
   <strong><em>Figure 4 – Visualization of Flooded and Non-Flooded Edges</em></strong>
</div>

<br> <!-- Spazio extra tra figura e testo -->

Figure 4 provides a visualization of several observations in their final states, where grey edges are non-flooded, purple edges are `flooded_init`, and cyan edges are `flooded_final`.

This visualization aids in understanding flood progression.

---

## OBJECTIVE

The task is to develop a predictive model that can accurately forecast the `flooded_final` status for each sample in the test set (`./test`). This project offers insight into real-world machine learning challenges, where achieving ideal results is often difficult. The emphasis is on the originality and soundness of the approach rather than solely on prediction accuracy.
