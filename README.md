# Biotope area factor Calculator

The **Biotopflächenfaktor (BAF) Calculator** is a VC Map plugin for evaluating the ecological quality of selected planning areas. It calculates the area, weighted biotope area, and resulting BAF for polygon features, groups the results by surface type, and presents them in a result table.

The plugin is part of the [VC Map Project](https://github.com/virtualcitySYSTEMS/map-ui).

## Features

- Calculate weighted biotope areas and the resulting BAF.
- Process selected planning layers from an active planning context.
- Aggregate areas and biotope areas by surface type.
- Display individual values, totals, weights, and the BAF in VC Map.
- Export a multi-page PDF report containing a map screenshot and result table.
- Optionally upload PDF, JSON, CSV, and GeoJSON analysis files to MinIO.
- Optionally register uploaded results as an IDRA/DCAT-AP catalogue dataset.

## Typical Workflow

1. Open a planning area in VC Map.
2. Select the planning layers to include, or use all available planning layers.
3. Run the BAF calculation.
4. Review the aggregated result table and BAF.
5. Export the result as a PDF report.
6. Optionally upload the analysis files and register the dataset in a catalogue.

## Required Data

The calculation expects polygon features in VC Map planning layers. Each feature must provide:

- `metadata.baf_weight`: numeric BAF weighting value.
- `metadata.greenType`: surface type used for grouping results.
- `metadata.key`: surface-type key.

Features without `metadata.baf_weight` are skipped. The plugin currently processes polygon geometries only.

## Optional Inputs

- `selected_layer_names`: planning layers to process. By default, all discovered layers are used.
- `upload_suffix`: suffix for uploaded file names and folders. The default is `Baseline`.
- `minio_endpoint`: MinIO proxy endpoint. The default is `https://urbreath.virtualcitymap.de/minioproxy`.
- `minio_bucket_name`: MinIO bucket. The default is `vcs-analysis`.
- `catalogue_endpoint`: endpoint used for optional catalogue registration.

## Outputs

- **BAF result table**: aggregated area, weight, biotope area, and overall BAF.
- **PDF report**: multi-page report with a map screenshot and result table.
- **Analysis summary**: optional JSON and semicolon-separated CSV exports.
- **BAF GeoJSON**: optional GeoJSON `FeatureCollection` containing analysed polygons and result attributes.
- **Catalogue dataset**: optional catalogue registration with described distributions.

## Supported Scope

The plugin is intended for:

- Municipalities
- Urban planners
- Landscape planners
- Environmental assessors

It can be used at site, block, neighbourhood, and district scale. Relevant climate-adaptation topics include urban greening, soil sealing, biodiversity, rainwater infiltration, green roofs, and climate adaptation.

## Limitations

- Only polygon geometries are included in the calculation.
- Features without `metadata.baf_weight` are skipped.
- Missing surface-type and key values are not validated.
- Overlapping polygons are not removed and may be counted more than once.
- The BAF is undefined for an empty selection or a total area of zero.
- The context menu and PDF map screenshot require an active Cesium map.
- Upload and catalogue registration require network access and compatible MinIO and IDRA endpoints.
- Catalogue distribution links are rewritten using fixed URBREATH URL prefixes.
- The plugin does not classify aerial imagery or surfaces without existing BAF metadata.
- It is not intended for lines, points, multipolygon geometries, or large-scale ecosystem modelling.
- Results are not a legally binding assessment without expert review of the input data and weighting values.

## Requirements

- [VC Map UI 6](https://github.com/virtualcitySYSTEMS/map-ui)
- VC Map Core with Cesium and OpenLayers
- MinIO Console API for optional file uploads
- IDRA/DCAT-AP catalogue API for optional catalogue registration

## Development

Install dependencies:

```bash
npm install
```

Build the plugin:

```bash
npm run build
```

Start the local development server:

```bash
npm start
```

Run the test suite:

```bash
npm test
```

Run type checking and linting:

```bash
npm run type-check
npm run lint
```

Create a production bundle:

```bash
npm run bundle
```

## Project Information

- Plugin ID: `baf-calculator`
- Version: `1.0.0`
- Maturity: Beta

## Further Reading

- [Calculating the Biotope Area Factor](https://www.berlin.de/sen/uvk/en/nature-and-green/landscape-planning/baf-biotope-area-factor/calculating-the-baf/)
- [BAF calculation examples](https://www.berlin.de/sen/uvk/en/nature-and-green/landscape-planning/baf-biotope-area-factor/calculation-examples/)
