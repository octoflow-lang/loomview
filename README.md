# LoomView

GPU-accelerated data visualization for OctoFlow.

One import, one function call — instant adaptive visualization.

## Quick Start

```octoflow
// Auto-detect the best visualization for your data
use "loomview"
viz_show([1.0, 4.0, 2.0, 8.0, 5.0, 7.0])
```

## Usage

### Auto Mode
```octoflow
use "loomview"
viz_show(my_data)    // fingerprints data, picks best chart type
```

### Explicit Mode
```octoflow
use "loomview"
viz_line(data)                // line chart
viz_bar(data)                 // bar chart
viz_scatter(xy_pairs)         // scatter plot (flat [x0,y0,x1,y1,...])
viz_heat(data, 40, 30)        // heatmap (w x h grid)
viz_histogram(data, 20)       // histogram with 20 bins
viz_pie(data)                 // pie chart
viz_grid(data, 10, 10)        // binary/integer grid
viz_genome(data)              // sequence visualization
```

### Recipe Mode
```octoflow
use "recipes/recipe_heat"
recipe_heat_run(60, 40)       // 2D heat diffusion

use "recipes/recipe_wave"
recipe_wave_run(60, 40)       // 2D wave propagation

use "recipes/recipe_nbody"
recipe_nbody_run(100)         // N-body gravitational simulation

use "recipes/recipe_mandelbrot"
recipe_mandelbrot_run()       // fractal zoom

use "recipes/recipe_sort_viz"
recipe_sort_run(80)           // sorting algorithm race

use "recipes/recipe_fft_viz"
recipe_fft_run()              // live spectrogram
```

### Interactive Controls

All visualizations support:
- **Pan**: click and drag to move the viewport
- **Zoom**: scroll wheel or +/- to zoom in/out
- **Inspect**: click a data point for value tooltip
- **Brush select**: drag a rectangle to highlight a region
- **Reset**: press R to reset the view

### Record & Save

Record your visualization session and export as a shareable file:

```octoflow
use "loomview"
use "src/recorder"

// Start recording
recorder_start(10.0)          // 10 FPS capture rate

// ... run your visualization ...

// Stop and export
recorder_stop()
recorder_export_gif("output.gif")     // animated GIF
recorder_export_html("output.html")   // self-contained HTML (plays in any browser)
recorder_export_csv("output.csv")     // raw data dump
```

Or use the toolbar: click the record button, interact with your visualization, then File > Export.

## 10 Visualization Types

| Type | Best For | Data Shape |
|------|----------|------------|
| Line | Trends, time series | Sequential values |
| Scatter | Correlations, clusters | [x0,y0, x1,y1, ...] pairs |
| Bar | Categories, comparisons | Small N values |
| Heatmap | 2D grids, matrices | w*h flat array |
| Histogram | Distributions | Continuous values |
| Pie | Proportions | Small N positive values |
| Sparkline | Dense time series | Large N sequential |
| Particles | Position data | [x,y] pairs |
| Grid | Binary/integer matrices | 0/1 or integer values |
| Genome | Sequences, evolution | Fixed-length bounded |

## Architecture

LoomView uses a 16-dimension fingerprinting system to auto-select the best visualization for any dataset. The fingerprint captures: length, range, mean, std, skewness, sparsity, periodicity, clusters, outliers, monotonicity, entropy, integer/binary/bounded flags, and unique ratio.

5 scientific color palettes: Viridis, Plasma, Inferno, Coolwarm, Grayscale.

## License

MIT
