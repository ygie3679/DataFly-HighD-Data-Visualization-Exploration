# DataFly: High-Dimensional Data Visualization Platform
Visit our platform: [https://datafly-high-dimensional-data.onrender.com/](https://datafly-high-dimensional-data.onrender.com/)

**DataFly** is a comprehensive web-based platform designed to explore and visualize high-dimensional datasets through advanced dimensionality reduction techniques. The system provides interactive 3D visualizations that help users discover patterns, relationships, and structures in complex data by projecting them into intuitive lower-dimensional spaces.

---

## Key Features

### Core Functionality
- **Multi-Algorithm Support**: Implements PCA, t-SNE, UMAP, and PCA-based t-SNE for comprehensive dimensionality reduction
- **Interactive 3D Visualization**: Real-time 3D scatter plots with smooth transitions between projections
- **Graph Network Support**: Visualize network data with nodes and edges, including support for GraphViz (.gv) files
- **Stress Analysis**: Advanced stress calculations for projection quality assessment
- **Triplet Exploration**: Systematic exploration of 3D projections with variance and stress metrics
- **Demo Datasets**: Built-in datasets for immediate exploration and testing

### Data Processing Capabilities
- **Multi-Format Support**: CSV, Excel, JSON, TXT, and GraphViz (.gv) files
- **Large Dataset Optimization**: Efficient processing for datasets with 40,000+ points
- **Automatic Preprocessing**: Data type optimization, missing value handling, and feature selection
- **Edge File Integration**: Optional edge files for network visualization
- **Label Management**: Automatic label generation or custom label support

### Advanced Visualization Features
- **Dynamic Projection Selection**: Interactive sliders for dimension selection
- **Color Mapping**: Automatic color schemes based on principal components or density
- **Interactive Metrics Chart**: Real-time visualization of projection quality with multiple metrics:
  - **Variance Analysis**: Shows 1-Variance scores for each projection viewpoint
  - **Stress Analysis**: Displays Shepard stress calculations for projection quality assessment
  - **On-Demand Additional Metrics**: Click legend to load additional quality measures:
    - **t-SNE Loss**: PCA-based t-SNE stress calculation
    - **Spring-Electrical Energy**: Graph layout energy optimization metric
    - **Edge Crossing**: Number of edge crossings in the projection
    - **Angular Resolution**: Minimum angle between edges at nodes
    - **Length Variation**: Coefficient of variation for edge lengths
- **Chart Interaction**: Click points on the metrics chart to jump to specific viewpoints
- **Special Viewpoint Highlighting**: Automatic identification and highlighting of:
  - Highest variance (Lowest 1-variance) viewpoint (gold highlighting)
  - Lowest stress viewpoint (green highlighting)
- **Smooth Animation**: Automated transitions between different projection views with DataFly mode
- **Pause and Resume**: Interactive control over visualization flow

---

## Supported File Formats

| File Type | Extensions | Requirements | Purpose |
|-----------|------------|--------------|---------|
| **GraphViz Files** | .gv | Valid GraphViz format | Complete graph definition with layout |

*Files below are currently not supported, and logic for this part was temporarily removed, but will continue to support in future versions*

| File Type | Extensions | Requirements | Purpose |
|-----------|------------|--------------|---------|
| **Data File** | CSV, XLSX, XLS, JSON, TXT | At least 2 numeric columns; optional label column | Primary dataset for analysis |
| **Edge File** | CSV, XLSX, XLS, JSON, TXT | Two columns: source_node, target_node | Network connections (optional) |

### Special Features for GraphViz (.gv) Files
- **Layout Algorithm Support**: Neato and SFDP layout algorithms
- **Multi-Dimensional Coordinate Extraction**: Configurable dimension extraction (default: 10D)
- **Automatic Node Processing**: Label extraction and coordinate generation
- **Network Analysis**: Integration with NetworkX for advanced graph metrics

---

## Dimensionality Reduction Algorithms

### Principal Component Analysis (PCA)
- **Explained Variance Analysis**: Detailed variance contribution per component
- **Adaptive Component Selection**: Automatic determination of optimal component count
- **Triplet Generation**: Systematic 3D projection combinations
- **Stress Calculation**: Shepard stress analysis for projection quality

### t-Distributed Stochastic Neighbor Embedding (t-SNE)
- **Adaptive Parameters**: Automatic perplexity and learning rate adjustment
- **3D Embeddings**: Full 3D t-SNE projections
- **Performance Optimization**: Efficient processing for large datasets

### Uniform Manifold Approximation and Projection (UMAP)
- **Density-Based Analysis**: Projection quality based on feature density
- **Memory Optimization**: Low-memory mode for large datasets
- **Robust Fallback**: Gaussian random projection backup

### PCA-based t-SNE
- **Hybrid Approach**: t-SNE applied to PCA-reduced data
- **Scalable Processing**: Efficient for high-dimensional datasets
- **Variance Integration**: Combined PCA variance and t-SNE stress analysis

---

### Basic Workflow

1. **Data Input:**
   - Upload your dataset (gv file required)
   - Or select from available demo datasets directly (no need to upload)

2. **Algorithm Selection:**
   - Choose from PCA, t-SNE, UMAP, or PCA-based t-SNE
   - For GraphViz files, select layout algorithm (Neato or SFDP)

3. **Projection Exploration:**
   - Monitor variance and stress metrics, and select points on the chart to go to specific viewpoints 
   - Use interactive sliders to select specific projections
   - View automated triplet sequences with DataFly mode

4. **Visualization Control:**
   - Pause/resume automatic transitions by hovering over DataFly button
   - Click "Go" for immediate projection updates
   - Use "Reset" to clear current analysis

### Advanced Features

- **Triplet Analysis**: Explore systematic combinations of 3D projections ranked by variance and stress
- **Interactive Metrics Dashboard**: Real-time chart showing multiple projection quality measures
- **On-Demand Metric Calculation**: Additional metrics calculated only when requested to optimize performance
- **Special Viewpoint Detection**: Automatic identification of optimal projections based on variance and stress
- **Large Dataset Mode**: Automatic optimization for datasets with 15,000+ points
- **Network Visualization**: Integrated edge rendering for graph data with specialized graph metrics

---

## Demo Datasets

| Dataset | Description | Features |
|---------|-------------|----------|
| **dwt1005_neato_10D** | Graph network dataset | 10 dimensions, 1,005 nodes, neato layout |
| **dwt992_neato_10D** | Graph network dataset | 10 dimensions, 992 nodes, neato layout |
| **dwt992_sfdp_10D** | Graph network dataset | 10 dimensions, 992 nodes, SFDP layout |
| **man5976_neato_10D** | Large graph dataset | 10 dimensions, 5,976 nodes, neato layout |

---
## DataFly 
   - To pause and view the current pair, hover over the **DataFly** button. The visualization will pause at the 
   current pair. Removing the hover will resume the transition to the next pairs.
   - The **DataFly** visualization automatically pauses when you:
     - Adjust the sliders to select specific projections.
     - Click the **Go** button to view the selected pair.
     - Switch the algorithm.



## Technical Architecture

### Backend Components
- **Flask Application:** Core web framework with SocketIO support
- **Data Processing Pipeline:** Pandas-based preprocessing with type optimization
- **Algorithm Implementations:** Scikit-learn, UMAP-learn integration
- **Graph Processing:** NetworkX and PyGraphviz for .gv file handling
- **Performance Optimization:** Memory-efficient processing for large datasets

### Frontend Features
- **Three.js WebGL Visualization Engine:** High-performance 3D rendering with hardware acceleration
- **Real-time Updates:** Dynamic projection updates without page refresh
- **Interactive Camera Controls:** OrbitControls for smooth navigation (rotation, zoom, pan)
- **Raycasting Mouse Interaction:** Precise point selection and tooltip display
- **Smooth Animation System:** Custom interpolation for seamless transitions between projections
- **Responsive Interface:** Adaptive UI for different screen sizes
- **Progress Monitoring:** Visual feedback for long-running computations

---

## Performance Considerations

- **Memory Management:** Automatic subsampling for datasets > 15,000 points
- **Computational Optimization:** Parallel processing where possible
- **Stress Calculation Sampling:** Intelligent sampling for large datasets (> 15,000 points)
- **Component Limitation:** Adaptive component selection based on dataset size

---

## License

This project is available under the MIT License. See the LICENSE file for more details.

---

## Future Roadmap

- **Additional Algorithms:** ISOMAP, Locally Linear Embedding (LLE)
- **Interactive Graph Editing:** Real-time node and edge manipulation
- **Cloud Integration:** Support for cloud-based dataset storage
- **Export Capabilities:** High-resolution image and data export
- **Advanced Metrics:** Additional projection quality measures
- **Real-time Collaboration:** Multi-user visualization sessions
