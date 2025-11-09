# Discordia Historical Data Repository

This repository contains historical data sources for the [Discordia](https://github.com/al1ce23/discordia) chaos monitoring system.

## 📊 Data Sources

### 1. EM-DAT (Emergency Events Database)

- **Location**: `disasters/nature/` and `disasters/tech/`
- **Source**: https://www.emdat.be/
- **Coverage**: 1900 - present
- **Update Frequency**: Continuously updated by CRED
- **Content**:
  - **Natural disasters**: Earthquakes, floods, storms, droughts, wildfires, volcanic eruptions, etc.
  - **Technological disasters**: Industrial accidents, transport accidents, miscellaneous accidents
- **Format**: Excel (.xlsx)
- **License**: Free for non-commercial research use (citation required)

**Citation**:
> EM-DAT, CRED / UCLouvain, Brussels, Belgium – www.emdat.be (D. Guha-Sapir)

**Current files**:
- `disasters/nature/public_emdat_custom_request_2025-10-24.xlsx` (~17,565 events)
- `disasters/tech/public_emdat_custom_request_2025-10-24.xlsx` (~9,697 events)

### 2. UCDP GED (Uppsala Conflict Data Program - Georeferenced Event Dataset)

- **Location**: `conflicts/`
- **Source**: https://ucdp.uu.se/downloads/
- **Coverage**: 1989 - 2024
- **Update Frequency**: Annually (version 25.1 current)
- **Content**:
  - Armed conflict events worldwide
  - State-based conflicts
  - Non-state conflicts
  - One-sided violence events
- **Format**: CSV
- **License**: Creative Commons BY-NC 4.0

**Citation**:
> Sundberg, Ralph, and Erik Melander, 2013, "Introducing the UCDP Georeferenced Event Dataset", Journal of Peace Research, vol.50, no.4, 523-532

**Current files**:
- `conflicts/GEDEvent_v25_1.csv` (~385,918 events, 3.96M fatalities documented)
- `conflicts/ged251-csv.zip` (compressed version)

## 📁 Directory Structure

```
historical_data/
├── conflicts/
│   ├── GEDEvent_v25_1.csv          # UCDP conflict events (1989-2024)
│   └── ged251-csv.zip               # Compressed version
├── disasters/
│   ├── nature/
│   │   └── public_emdat_*.xlsx      # EM-DAT natural disasters
│   ├── tech/
│   │   └── public_emdat_*.xlsx      # EM-DAT technological disasters
│   └── README.md                     # Import guide and documentation
├── README_SUBMODULE.md               # This file
└── .gitignore
```

## 🔧 Usage as Submodule

This repository is designed to be used as a Git submodule in the main Discordia project.

### Initial Setup (for developers)

**Cloning the main project with submodules**:
```bash
git clone --recursive https://github.com/al1ce23/discordia.git
```

**Or if already cloned without submodules**:
```bash
cd discordia
git submodule init
git submodule update
```

### Updating Data

**Pull latest data**:
```bash
cd discordia/historical_data
git pull origin main
```

**Update main project to use latest data**:
```bash
cd ..
git add historical_data
git commit -m "Update historical data to latest version"
git push
```

### Contributing New Data

1. Add new data files to appropriate directory
2. Update this README with file information
3. Commit and push to this repository
4. Update the main project's submodule reference

```bash
cd historical_data
git add .
git commit -m "Add [description of new data]"
git push

cd ..
git add historical_data
git commit -m "Update historical_data submodule reference"
git push
```

## 📥 Data Import to Discordia

### EM-DAT Disasters

```bash
# Inspect data structure
python -m core.importers.emdat_disasters \
  --file historical_data/disasters/nature/public_emdat_*.xlsx \
  --inspect

# Import natural disasters
python -m core.importers.emdat_disasters \
  --file historical_data/disasters/nature/public_emdat_*.xlsx

# Import technological disasters
python -m core.importers.emdat_disasters \
  --file historical_data/disasters/tech/public_emdat_*.xlsx
```

### UCDP Conflict Events

```bash
# Inspect data structure
python -m core.importers.ucdp_conflicts \
  --file historical_data/conflicts/GEDEvent_v25_1.csv \
  --inspect

# Import conflict events
python -m core.importers.ucdp_conflicts \
  --file historical_data/conflicts/GEDEvent_v25_1.csv \
  --batch-size 500
```

See [disasters/README.md](disasters/README.md) for detailed import instructions.

## 📊 Data Statistics

### EM-DAT Coverage

**Natural Disasters**:
- Total events: ~17,565
- Date range: 1900 - 2025
- Top types: Floods, Storms, Earthquakes, Droughts
- Total deaths: Millions
- Total affected: Billions

**Technological Disasters**:
- Total events: ~9,697
- Date range: 1900 - 2025
- Top types: Industrial fires/explosions, Transport accidents
- Total deaths: Hundreds of thousands

### UCDP GED Coverage

- Total events: 385,918
- Date range: 1989-01-01 to 2024-12-31
- Total documented fatalities: ~3.96 million
- Event types:
  - State-based conflicts: 271,331 events
  - Non-state conflicts: 54,982 events
  - One-sided violence: 59,605 events
- Top affected countries: Syria, Afghanistan, Ukraine, Mexico, India

## 🗂️ File Sizes

| File | Size | Records |
|------|------|---------|
| GEDEvent_v25_1.csv | ~150 MB | 385,918 |
| ged251-csv.zip | ~30 MB | - |
| EM-DAT nature .xlsx | ~5 MB | 17,565 |
| EM-DAT tech .xlsx | ~3 MB | 9,697 |

**Total repository size**: ~160 MB

## 🔄 Update Schedule

- **UCDP GED**: Check for updates annually at https://ucdp.uu.se/downloads/
- **EM-DAT**: Download updated exports quarterly from https://www.emdat.be/

## 📜 Licensing & Citations

### EM-DAT Terms

- Free for non-commercial research
- Attribution required
- Do not redistribute without permission
- Cite as: EM-DAT, CRED / UCLouvain, Brussels, Belgium – www.emdat.be

### UCDP GED Terms

- Creative Commons BY-NC 4.0
- Attribution required
- Non-commercial use
- Cite the dataset and relevant publications

## 🐛 Issues & Contributions

Report issues or suggest new data sources:
- **Main project issues**: https://github.com/al1ce23/discordia/issues
- **Data-specific issues**: https://github.com/al1ce23/discordia-historical-data/issues

## 🔗 Related Links

- [Discordia Main Repository](https://github.com/al1ce23/discordia)
- [EM-DAT Database](https://www.emdat.be/)
- [UCDP GED Dataset](https://ucdp.uu.se/downloads/)
- [Import Documentation](disasters/README.md)

## 📝 Version History

- **v1.0.0** (2025-01): Initial repository setup
  - EM-DAT natural disasters (17,565 events, 1900-2025)
  - EM-DAT technological disasters (9,697 events, 1900-2025)
  - UCDP GED v25.1 (385,918 events, 1989-2024)

---

**Maintained as part of the Discordia Project**
