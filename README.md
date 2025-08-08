# Hexagonal Grid-Based Localization using Adaptive Monte Carlo Localization

[![ROS Version](https://img.shields.io/badge/ROS-Noetic-blue.svg)](http://wiki.ros.org/noetic)
[![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)

A novel implementation of Adaptive Monte Carlo Localization (AMCL) using hexagonal grid systems for improved robot localization accuracy in simulated environments.

## 🎯 Overview

This project presents a comprehensive investigation of AMCL implemented on hexagonal grid systems compared to traditional square grid frameworks. Our hexagonal grid mapping approach leverages the isotropic connectivity properties of hexagonal tessellation to achieve:

- **23% improved localization accuracy**
- **18% faster convergence** 
- Superior performance on curved trajectory following

## ✨ Key Features

- **Novel Hexagonal Grid Implementation**: Custom hexagonal grid system using axial coordinates
- **Enhanced AMCL Algorithm**: Modified particle filter for hexagonal grid compatibility
- **Comprehensive Evaluation**: Statistical analysis across multiple trajectory types
- **ROS Integration**: Full compatibility with Robot Operating System
- **Open Source Framework**: Extensible codebase for research applications

## 📊 Performance Comparison

| Metric | Square Grid | Hexagonal Grid | Improvement |
|--------|-------------|----------------|-------------|
| Linear Path Error | 4.2 ± 1.1 cm | 3.8 ± 0.9 cm | 9.5% |
| Curved Path Error | 7.8 ± 2.3 cm | 5.7 ± 1.6 cm | 26.9% |
| Complex Path Error | 9.1 ± 2.8 cm | 7.2 ± 2.1 cm | 20.9% |
| Convergence Time | Baseline | 18% faster | - |

## 🛠️ Installation

### Prerequisites

- ROS Noetic
- Gazebo 11
- Python 3.8+
- NumPy, SciPy, Matplotlib

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/hexagonal-grid-amcl.git
   cd hexagonal-grid-amcl
   ```

2. **Create a catkin workspace**
   ```bash
   mkdir -p ~/catkin_ws/src
   cd ~/catkin_ws/src
   ln -s /path/to/hexagonal-grid-amcl .
   ```

3. **Install dependencies**
   ```bash
   cd ~/catkin_ws
   rosdep install --from-paths src --ignore-src -r -y
   ```

4. **Build the package**
   ```bash
   catkin_make
   source devel/setup.bash
   ```

## 🚀 Quick Start

### Running the Simulation

1. **Launch the Gazebo environment**
   ```bash
   roslaunch hexagonal_amcl gazebo_world.launch
   ```

2. **Start the hexagonal AMCL node**
   ```bash
   roslaunch hexagonal_amcl hexagonal_amcl.launch
   ```

3. **Run trajectory evaluation**
   ```bash
   rosrun hexagonal_amcl trajectory_evaluator.py --path curved
   ```

### Available Test Scenarios

- `linear`: Straight-line trajectory across the environment
- `curved`: Smooth curved trajectory with varying curvature  
- `complex`: Mixed trajectory with sharp turns and curves

## 📁 Project Structure

```
hexagonal-grid-amcl/
├── src/
│   ├── hexagonal_amcl/
│   │   ├── hexagonal_grid.py      # Core hexagonal grid implementation
│   │   ├── amcl_node.py          # Modified AMCL algorithm
│   │   ├── sensor_model.py       # Hexagonal ray-casting
│   │   └── coordinate_utils.py   # Coordinate transformations
│   ├── evaluation/
│   │   ├── trajectory_evaluator.py
│   │   └── statistical_analysis.py
│   └── visualization/
│       ├── grid_visualizer.py
│       └── particle_display.py
├── launch/
│   ├── hexagonal_amcl.launch
│   └── gazebo_world.launch
├── config/
│   ├── amcl_params.yaml
│   └── sensor_config.yaml
├── worlds/
│   └── test_environment.world
├── docs/
│   ├── paper.pdf
│   └── API_documentation.md
└── results/
    ├── performance_data.csv
    └── visualization_plots/
```

## 🔬 Research Methodology

### Hexagonal Grid Representation

The system uses axial coordinates (q, r) for hexagonal tessellation:

```
q = (2/3) * (x/size)
r = (-1/3) * (x/size) + (√3/3) * (y/size)
```

### AMCL Algorithm Adaptation

Key modifications include:
- Hexagonal coordinate particle initialization
- Modified sensor model with hexagonal ray-casting
- Uniform 6-connectivity neighbor relationships

### Evaluation Metrics

- **Localization Error**: Euclidean distance between true and estimated pose
- **Convergence Time**: Time to stabilize below error threshold
- **Computational Efficiency**: Processing time and memory usage

## 📈 Results

The hexagonal grid approach demonstrates significant improvements, particularly for curved trajectories where the isotropic properties provide superior spatial representation. Statistical analysis confirms significance across all test scenarios (p < 0.01).

## 🔄 Usage Examples

### Basic Localization

```python
from hexagonal_amcl import HexagonalAMCL

# Initialize hexagonal AMCL
amcl = HexagonalAMCL(
    grid_size=0.1,
    num_particles=500,
    map_file="test_environment.pgm"
)

# Process sensor data
pose_estimate = amcl.update(laser_scan, odometry)
```

### Custom Trajectory Evaluation

```python
from evaluation.trajectory_evaluator import TrajectoryEvaluator

evaluator = TrajectoryEvaluator()
results = evaluator.run_scenario(
    scenario_type="curved",
    num_trials=50,
    grid_type="hexagonal"
)
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📚 Documentation

- [API Documentation](docs/API_documentation.md)
- [Research Paper](docs/paper.pdf)
- [Algorithm Details](docs/algorithm_details.md)
- [Performance Benchmarks](docs/benchmarks.md)

## 🐛 Known Issues

- Approximately 20% computational overhead compared to square grids
- 17% increase in memory usage for map storage
- Requires additional coordinate transformation computations

## 🔮 Future Work

- [ ] Adaptive hexagon sizing based on environment complexity
- [ ] Integration with SLAM algorithms
- [ ] Real-world validation with physical robots
- [ ] Extension to 3D hexagonal tessellation
- [ ] GPU acceleration for improved performance

## 📄 Citation

If you use this work in your research, please cite:

```bibtex
@article{singh2025hexagonal,
  title={Hexagonal Grid-Based Localization using Adaptive Monte Carlo Localization in Simulated Robotic Environments},
  author={Singh, Aditi and Kadam, Pratham},
  journal={T.B.A},
  year={2025}
}
```

## 👥 Authors

- **Aditi Singh** - *Lead Researcher* - [aditi.chauhannn.n@gmail.com](mailto:aditi.chauhannn.n@gmail.com)
- **Pratham Kadam** - *Co-Researcher* - [prathamakadam2003@gmail.com](mailto:prathamakadam2003@gmail.com)

## 🙏 Acknowledgments

- Faculty at Parul Institute of Engineering and Technology
- ROS and Gazebo communities
- Open-source robotics community

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Related Projects

- [Traditional AMCL Implementation](https://github.com/ros-planning/navigation)
- [Hexagonal Grid Algorithms](https://github.com/redblobgames/hexagons)
- [ROS Navigation Stack](https://github.com/ros-planning/navigation2)

---

⭐ **Star this repository if you find it useful!** ⭐
