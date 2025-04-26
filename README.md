## Welcome to Multi-Sensor Defense Analysis Platform (MSDAP)
MSDAP is a platform designed to analyze threats of LiDAR attacks in autonomous driving security, developed as an open-source tool. It operates on the AWSIM and Autoware Universe foundation, developed by Autoware Foundation (https://autoware.org/).

## Overview
MSDAP provides a comprehensive simulation environment for analyzing and testing LiDAR-based attack scenarios in autonomous driving systems. The platform enables researchers and developers to:
- Simulate various types of LiDAR attacks
- Analyze attack impacts on autonomous driving systems
- Develop and test defense mechanisms
- Evaluate system robustness against attacks

## Features
This extension provides the following features:

### HFR (High Frequency Removal) Attack Simulation
- Simulates attacks that remove LiDAR point cloud data
- Configurable elimination angle for attack simulation
- Adjustable success rate for attack simulation
- CSV-based success rate matrix configuration

### CPI (Chosen Point Injection) Attack Simulation
- Simulates attacks that inject false LiDAR point cloud data
- Configurable injection parameters
- Real-time attack simulation

### Visualization
- Real-time visualization of attack effects
- Comparison between attacked and unattacked point clouds

unattacked point cloud<br>
![benign](https://github.com/user-attachments/assets/013ca6bf-cf5a-4cac-950b-368c9e6e9264)

attacked point cloud<br>
![attacked](https://github.com/user-attachments/assets/730c1716-7615-4a40-a606-fbde33c9ab89)

## Prerequisites
- Ubuntu 22.04 LTS
- ROS 2 Humble
- AWSIM (Driving Simulator)
- Autoware Universe 
- Python 3.8 or higher
- Eigen3 library

## Installation

### 1. System Setup
```bash
# Install system dependencies
sudo apt update
sudo apt install -y python3-pip python3-colcon-common-extensions
```

### 2. Install AWSIM
Follow the official installation guide:
https://tier4.github.io/AWSIM/GettingStarted/SetupUnityProject/

### 3. Install Autoware Universe
Follow the official installation guide:
https://tier4.github.io/AWSIM/GettingStarted/QuickStartDemo/

### 4. Install MSDAP
```bash
# Create workspace if it doesn't exist
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

# Clone the repository
git clone git@github.com:Ofurosuki/lidar_attack_simulator.git

# Build the package
cd ~/ros2_ws
colcon build --symlink-install
```

## Usage

### 1. Environment Setup
```bash
# Source ROS2 underlay
source /opt/ros/humble/setup.bash

# Source the ROS2 package
cd ~/ros2_ws
source install/setup.bash
```

### 2. Configuration
Edit the launch file parameters in `hfr_simulator_launch.py` or `cpi_simulator_launch.py`:

```python
# Example parameters for HFR simulator
hfr_simulator = Node(
    package='attack_simulator',
    executable='hfr_simulator',
    parameters=[
        {'elimination_angle': 20.0},  # Angle in degrees
        {'success_rate_chrono': 0.1},  # Success rate for attack
        {'csv_path': '/path/to/success_rate_matrix.csv'}  # Path to success rate matrix
    ]
)
```

### 3. Launch the Simulator
```bash
# For HFR attack simulation
ros2 launch attack_simulator hfr_simulator.launch.py

# For CPI attack simulation
ros2 launch attack_simulator cpi_simulator.launch.py
```

## Parameters

### HFR Simulator Parameters
- `elimination_angle`: Angle in degrees for point cloud elimination (default: 20.0)
- `success_rate_chrono`: Success rate for attack simulation (default: 0.1)
- `csv_path`: Path to CSV file containing success rate matrix

### CPI Simulator Parameters
- `injection_rate`: Rate of point cloud injection (default: 0.1)
- `injection_distance`: Distance for point injection (default: 10.0)
- `injection_angle`: Angle for point injection (default: 30.0)

## Troubleshooting

### Common Issues
1. **Build Errors**
   - Ensure all dependencies are installed
   - Check ROS2 environment is properly sourced
   - Verify Eigen3 is installed

2. **Runtime Errors**
   - Check parameter values in launch files
   - Verify CSV file paths and formats
   - Ensure AWSIM and Autoware are running

3. **Visualization Issues**
   - Check RViz configuration
   - Verify topic names and types

## Contributing
We welcome contributions to MSDAP! Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

Please ensure your code follows the project's coding standards and includes appropriate tests.

## License
This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Contact
For questions and support, please open an issue in the GitHub repository.

## Acknowledgments
- Autoware Foundation for AWSIM and Autoware Universe
- All contributors to this project



