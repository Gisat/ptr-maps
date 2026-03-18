[![Release](https://github.com/gisat-panther/ptr-maps/actions/workflows/release.yml/badge.svg?branch=master)](https://github.com/gisat-panther/ptr-maps/actions/workflows/release.yml)
[![.github/workflows/test.yml](https://github.com/gisat-panther/ptr-maps/actions/workflows/test.yml/badge.svg?branch=master)](https://github.com/gisat-panther/ptr-maps/actions/workflows/test.yml)

# ptr-maps

A React-based mapping library for the [Panther](https://github.com/gisat-panther) frontend framework. It provides WebGL-accelerated map rendering via [deck.gl](https://deck.gl), along with a set of map controls, layout components, and projection utilities.

## Installation

```bash
npm install @gisatcz/ptr-maps
```

### Peer dependencies

The following packages must be installed in your project:

```bash
npm install react react-dom
```

Supported versions: React `^16.13.1 || ^17.0.2 || ^18.3.1`

## Usage

```jsx
import {PresentationMap, DeckGlMap, MapControls} from '@gisatcz/ptr-maps';

<PresentationMap
	mapComponent={DeckGlMap}
	view={{center: {lat: 50, lon: 15}, boxRange: 100000}}
	backgroundLayer={{type: 'wmts', options: {url: '...'}}}
/>;
```

## Exported API

### Map components

| Export                  | Description                                                                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `PresentationMap`       | Core map component. Accepts any compatible `mapComponent` (e.g. `DeckGlMap`). Handles view state, resizing, and layer rendering.       |
| `DeckGlMap`             | WebGL-accelerated map built on [deck.gl v9](https://deck.gl). Supports raster tiles, WMS, vector, MVT, COG bitmap, and terrain layers. |
| `MapSet`                | Synchronises the view across multiple maps. Use `MapSetMap` / `MapSetPresentationMap` as child descriptors.                            |
| `MapSetMap`             | Child descriptor for a connected (state-driven) map inside `MapSet`.                                                                   |
| `MapSetPresentationMap` | Child descriptor for a presentation-only map inside `MapSet`.                                                                          |
| `MapGrid`               | Automatically arranges multiple maps in a responsive grid.                                                                             |
| `MapWrapper`            | Container that adds an optional title bar and a close button to a map.                                                                 |

### Controls

| Export                | Description                                                         |
| --------------------- | ------------------------------------------------------------------- |
| `MapControls`         | Zoom, tilt, and heading control buttons for the map view.           |
| `MapScale`            | Visual map scale bar calculated from the current view.              |
| `MapTools`            | Generic container for placing tool components over the map.         |
| `GoToPlace`           | Search input that triggers a navigation callback (`goToPlace`).     |
| `SimpleLayersControl` | Layer switcher drop-down for selecting a background layer template. |

### Loadable (code-split) variants

| Export                | Description                      |
| --------------------- | -------------------------------- |
| `LoadableMap`         | Lazily loaded `PresentationMap`. |
| `LoadableMapSet`      | Lazily loaded `MapSet`.          |
| `LoadableMapControls` | Lazily loaded `MapControls`.     |

### DeckGlMap layers

Layers are passed as objects in the `layers` / `backgroundLayer` props of `DeckGlMap` / `PresentationMap`.

| Layer type         | Description                                                                                                                               |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `TiledLayer`       | XYZ raster tile layer. Supports subdomain templates (`{s}`) and native zoom clamp. Optional terrain draping via `clampToTerrain`.         |
| `WmsLayer`         | OGC WMS layer rendered tile-by-tile. Supports pickable/hoverable tooltips, custom texture parameters, and transparent colour replacement. |
| `VectorLayer`      | GeoJSON / binary vector features layer. Supports selections, styling, and terrain draping.                                                |
| `MVTLayer`         | Mapbox Vector Tiles (MVT) layer with hover/selection highlight support.                                                                   |
| `TiledVectorLayer` | Tiled vector data layer (non-MVT).                                                                                                        |
| `CogBitmapLayer`   | Cloud-Optimised GeoTIFF (COG) raster layer (via `@gisatcz/deckgl-geolib`).                                                                |
| `CogTerrainLayer`  | COG-based terrain / elevation layer (via `@gisatcz/deckgl-geolib`).                                                                       |

### Utilities

| Export      | Description                                                                                                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `view`      | Helper functions for working with the Panther view model (`boxRange`, heading, tilt, etc.).                                                                                  |
| `proj`      | Projection utilities built on [proj4](https://proj4js.org/). Includes predefined UTM and Křovák definitions, and an `addProjections` function to register custom EPSG codes. |
| `constants` | Shared map constants.                                                                                                                                                        |

### Re-exports from deck.gl / luma.gl

For convenience the following deck.gl / luma.gl namespaces are re-exported:

| Export             | Source                |
| ------------------ | --------------------- |
| `GL`               | `@luma.gl/constants`  |
| `deckgl_core`      | `@deck.gl/core`       |
| `deckgl_layers`    | `@deck.gl/layers`     |
| `deckgl_geolayers` | `@deck.gl/geo-layers` |

## Key dependencies

| Package                  | Version |
| ------------------------ | ------- |
| `@deck.gl/*`             | ^9.0    |
| `@luma.gl/*`             | ^9.0    |
| `@loaders.gl/core`       | ^4.1    |
| `@gisatcz/deckgl-geolib` | 2.1.5   |
| `@gisatcz/ptr-core`      | ^1.8    |
| `@gisatcz/ptr-utils`     | ^1.6    |
| `@gisatcz/ptr-atoms`     | ^1.16   |
| `proj4`                  | ^2.15   |

## Development

```bash
# Build (ES module + CJS)
npm run build

# Watch mode
npm run start

# Run tests
npm test

# Run tests with coverage
npm run coverage

# Lint
npm run lint
```

## License

[Apache-2.0](LICENSE)
