# Square Cylinder - Cross-Geometry Prediction

This folder contains an experimental cross-geometry prediction: using a model trained on **circular** cylinders to predict **square** cylinder flow.

## ⚠️ Important Note
This is an **educational demonstration** showing the limitations of cross-geometry transfer learning. The model was trained on circular cylinders, so predictions for square cylinders have significant errors due to geometry mismatch.

## Contents

### Code Files
- **lbm_square_cylinder.cpp** - LBM simulation for square cylinder (C++)
- **predict_square_with_circular_model.py** - Cross-geometry prediction script (Python)
- **square_cylinder_cross_geometry.ipynb** - Complete Jupyter notebook with g++ installation

### Data Files
**Square Cylinder:**
- **square_cylinder_re35.txt** - LBM ground truth for square cylinder at Re=35

**Circular Cylinder (Training Data):**
- **circular_cylinder_re10.txt** - Training data
- **circular_cylinder_re20.txt** - Training data
- **circular_cylinder_re30.txt** - Training data

### Results
- **square_cylinder_cross_geometry_report.txt** - Complete analysis and comparison
- **square_cylinder_cross_geometry_prediction.png** - Visualization of geometry mismatch

## Quick Start

### Option 1: Run Jupyter Notebook (Recommended for Google Colab)
1. Open `square_cylinder_cross_geometry.ipynb` in Google Colab
2. The notebook includes:
   - g++ compiler installation for Colab
   - Complete C++ LBM code
   - PINN training and prediction
   - Comprehensive visualizations

### Option 2: Run Python Script
```bash
# Install dependencies
pip install deepxde matplotlib numpy

# Run cross-geometry prediction
python predict_square_with_circular_model.py
```

### Option 3: Run LBM Simulation Only
```bash
# Compile C++ code
g++ -O3 -std=c++11 lbm_square_cylinder.cpp -o lbm_square_cylinder

# Run simulation
./lbm_square_cylinder
```

## Results Summary

**Cross-Geometry Prediction (Square Cylinder Re=35):**
- MSE (u): 1.12e-04 (2.4x worse than circular)
- MSE (v): 4.08e-05 (8.7x worse than circular)
- Relative Error (u): 10.19%
- Relative Error (v): 68.06% (very high due to geometry mismatch)

**Comparison with Circular Cylinder Re=35:**
- Circular (same geometry): 6.58% u-error, 25.11% v-error
- Square (cross-geometry): 10.19% u-error, 68.06% v-error

## Key Observations
1. **Geometry mismatch significantly increases errors**
2. **V-component most affected** - square corners create different flow separation
3. **Circular model cannot capture sharp corner effects**
4. **Cross-geometry transfer learning has limitations**

## Educational Value
This experiment demonstrates:
- ✅ Models can generalize within same geometry (Re interpolation/extrapolation)
- ❌ Models cannot generalize across different geometries without specific training
- ⚠️ Importance of geometry-specific training data

## Recommendations
For accurate square cylinder predictions:
1. Generate LBM data for square cylinders at multiple Re
2. Train a new model specifically for square geometry
3. OR: Use shape-parametric model trained on both geometries
4. OR: Use transfer learning with fine-tuning on square cylinder data

## References
- DeepXDE: https://github.com/lululxvi/deepxde
- LBM: "Lattice Boltzmann Method: Fundamentals and Engineering Applications"
