# Terrain Generation Library

## Overview

This project provides a C++ library for procedural terrain generation using both Perlin noise and diamond-square algorithms. It's designed to create realistic heightmaps for games, simulations, or other applications requiring procedural terrain.

## Features

- **Perlin Noise Generation**: Includes 1D, 2D, 3D, and 4D Perlin noise functions with periodic variants
- **Diamond-Square Algorithm**: For fractal terrain generation with customizable roughness
- **Continent Generation**: Create multiple continents with proper spacing
- **Ocean Floor Generation**: Generate underwater terrain with Perlin noise
- **Sea Level Adjustment**: Control water coverage percentage
- **Seeding Support**: Reproducible results with seed-based generation
- **Smoothing Functions**: For refining generated terrain
- **Heightmap Manipulation**: Various utility functions for working with heightmaps

## Usage

### Basic Setup

1. Include the headers:
   ```cpp
   #include "TerrainGen.h"
   ```

2. Create a terrain generator instance:
   ```cpp
   ftg::TerrainGen terrainGen;
   ```

3. Seed the generator for reproducible results:
   ```cpp
   terrainGen.seed("my_seed_string");
   ```

### Generating Terrain

```cpp
// Create a heightmap (using Vector2D<float>)
SingleLayer heightmap(width, height);

// Generate ocean floor
terrainGen.generateOceanFloor(heightmap, width, height, slope, roughness);

// Add continents
terrainGen.generateContinents(heightmap, width, height, slope, roughness, numContinents);

// Adjust sea level (e.g., 0.3 for 30% water coverage)
terrainGen.setSeaLevel(heightmap, 0.3f, width, height);
```

### Advanced Features

- **Custom Heightmaps**: Use `generateHeightMap` for custom fractal terrain
- **Peak Generation**: Create mountain peaks with `makePeak`
- **Heightmap Combination**: Combine heightmaps with `addHeightMap`
- **Smoothing**: Apply smoothing passes with `smoothHeightMap`

## Building

1. Ensure you have the required dependencies:
   - A C++17 compliant compiler
   - The `Vector2D` template class (included in the project)

2. Include all source files in your project build:
   - `ImprovedPerlin.cpp`
   - `TerrainGen.cpp`

## Example

```cpp
#include "TerrainGen.h"

int main() {
    const short width = 513;
    const short height = 513;
    
    ftg::TerrainGen terrainGen;
    terrainGen.seed("world_seed");
    
    SingleLayer world(height, width);
    
    // Generate terrain
    terrainGen.generateOceanFloor(world, width, height, 100.0f, 0.5f);
    terrainGen.generateContinents(world, width, height, 500.0f, 0.7f, 5);
    terrainGen.setSeaLevel(world, 0.3f, width, height);
    
    // Use the heightmap...
    
    return 0;
}
```

## Performance Notes

- The diamond-square algorithm works best with map sizes of (2^n + 1)
- For large maps, consider generating in chunks
- The Perlin noise implementation is optimized for cache performance

## License

The Perlin noise implementation is public domain (as noted in the original header). The rest of the code can be used under the MIT license.
