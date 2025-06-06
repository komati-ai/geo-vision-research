---
language:
- en
- fr
pretty_name: "Canada Geological Maps Collection"
tags:
- geospatial
- geology
- maps
- canada
- mining
- surficial-geology
- mineral-exploration
license: other
task_categories:
- image-classification
- object-detection
- feature-extraction
size_categories:
- 10<n<100
modality:
- geospatial
- image
---

# Canada Geological Maps Collection

## Dataset Description

This dataset contains a collection of Canadian geological and mineral exploration maps from two primary sources: GEOSCAN (Geological Survey of Canada) and MINFILE (British Columbia Mineral Inventory). The dataset includes both historical and contemporary geological maps covering various provinces and territories across Canada.

### Dataset Summary

The Canada Geological Maps Collection provides researchers and practitioners with access to digitized geological maps spanning from 1961 to 2022. The maps include surficial geology, mineral exploration data, topographical surveys, and geophysical studies across Canadian provinces and territories.

- **Total Images**: ~16 maps (expandable collection)
- **Time Range**: 1961-2022  
- **Geographic Coverage**: Multiple Canadian provinces (BC, QC, ON, NS, NT, NU)
- **Map Types**: Surficial geology, mineral exploration, topographical, geophysical
- **Languages**: English and French

### Supported Tasks

- **Geospatial Analysis**: Extract geological features and formations
- **Historical Research**: Study evolution of geological understanding
- **Mining Exploration**: Access mineral deposit locations and geological context
- **Computer Vision**: Map feature detection and classification
- **GIS Integration**: Digitization and spatial analysis workflows

## Dataset Structure

### Data Fields

Each entry in the metadata contains:

- `name`: Official title of the geological map
- `type`: Category of geological information (e.g., "Surficial geology", "map - geophysical")
- `province`: Canadian province/territory code (bc, qc, on, ns, nt, nu)
- `year`: Publication year of the map
- `dir`: Relative path to the image file
- `doi`: Digital Object Identifier or reference URL

### File Organization

```txt
dataset/
├── images/
|   └── train/
│        ├── geoscan/          # Geological Survey of Canada maps
│        │   ├── gid_*/        # Individual map directories
│        │   └── gscmap-*/     # GSC map series
│        └── minfiles/         # BC MINFILE mineral exploration maps
│            └── */            # Individual property directories
├── metadata.jsonl        # Complete dataset metadata
└── README.md            # This dataset card
```

## Data Sources

### GEOSCAN

The GEOSCAN maps are obtained from the [GEOSCAN database](https://ostrnrcan-dostrncan.canada.ca/handle/1845/60977), which is Canada's national repository of earth science research and publications.

**License**: [Open Government Licence - Canada](https://open.canada.ca/en/open-government-licence-canada)

### MINFILE

The MINFILE maps are obtained from British Columbia's [MINFILE system](https://minfile.gov.bc.ca/), a comprehensive mineral deposit information system.

**Historical Context**: 
- [MINFILE - A Mineral Deposit Information System for British Columbia](https://cmscontent.nrs.gov.bc.ca/geoscience/publicationcatalogue/InformationCircular/BCGS_IC1992-02.pdf)
- [Project description](https://www2.gov.bc.ca/gov/content/industry/mineral-exploration-mining/british-columbia-geological-survey/mineralinventory/moreinfo)

## Usage Examples

### Loading the Dataset

```python
from datasets import load_dataset
import json

# Load metadata
with open('metadata.jsonl', 'r') as f:
    metadata = json.load(f)

# Filter by province
bc_maps = [item for item in metadata if item['province'] == 'bc']

# Filter by map type
surficial_maps = [item for item in metadata if 'surficial' in item['type'].lower()]
```

### Computer Vision Applications

```python
from PIL import Image
import os

# Load and process maps
for item in metadata:
    if os.path.exists(item['dir']):
        image = Image.open(item['dir'])
        print(f"Processing: {item['name']} ({item['year']})")
        # Your processing code here
```

## Dataset Creation

### Source Data Collection

Maps were systematically collected from:
1. **GEOSCAN**: Federal geological survey publications
2. **MINFILE**: Provincial mineral exploration records

### Data Processing

- Maps digitized and stored in JPG format
- Metadata extracted and structured in JSON format
- DOI/reference links preserved for traceability
- Consistent naming conventions applied

## Considerations for Use

### Ethical Considerations

- Maps may contain references to Indigenous territories and traditional knowledge
- Some geological information may be sensitive for environmental or security reasons
- Historical maps may contain outdated terminology or perspectives

### Limitations

- Dataset is currently incomplete and under active development
- Image quality varies based on source material age and digitization methods
- Some maps may have geographic projection inconsistencies
- Metadata completeness varies across entries

### Intended Use

This dataset is intended for:
- Academic research in geology and earth sciences
- Development of computer vision models for map analysis
- Historical studies of geological exploration in Canada
- Educational purposes in geology and GIS

### Out-of-Scope Use

- Commercial mining exploration without proper licensing
- Definitive geological assessments (always consult original sources)
- Legal boundary determinations

## Additional Information

### Dataset Curators

This dataset is maintained as part of geo-vision research initiatives.

### Licensing Information

- **GEOSCAN data**: [Open Government Licence - Canada](https://open.canada.ca/en/open-government-licence-canada)
- **MINFILE data**: Subject to British Columbia government data licensing
- **Dataset compilation**: Please cite appropriately when using this collection

### Citation

```bibtex
@dataset{canada_maps_dataset_2025,
  title={Canada Maps Dataset},
  author={Komati AI},
  year={2025},
  publisher={Hugging Face},
  url={https://huggingface.co/datasets/komati-ai/canada-maps-dataset}
}
```

### Contributions

We welcome contributions to expand this dataset. Please ensure all contributed maps include proper licensing and metadata information.

For questions or contributions, please open an issue in the dataset repository.

