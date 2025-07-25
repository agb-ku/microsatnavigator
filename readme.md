# MicrosatNavigator

A fast and efficient tool for identifying microsatellite repeat motifs in genome sequences, developed for large-scale analysis of vertebrate genomes.

## Installation

### Prerequisites
- Python 3.x
- C compiler (gcc/clang)
- Git

### Setup Instructions

1. **Clone the repository:**
```bash
git clone git@github.com:agb-ku/microsatnavigator.git
cd microsatnavigator
```

2. **Create and activate virtual environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install the C extension:**
```bash
cd py-extension/src
python setup.py install
```

4. **Install with pip (choose one):**
```bash
# Standard installation
pip install .

# Development installation (editable)
pip install -e .
```

5. **Verify installation:**
```bash
python -c "import microsatellite"
```

If no errors occur, the installation is successful.

### Install BioPython (if needed)
```bash
pip install biopython
```

## Quick Usage

### Basic microsatellite search:
```bash
python microsatnavigator.py --fasta input.fasta --output results.tsv
```

### For FASTQ files:
```bash
python microsatnavigator.py --fastq input.fastq --output results.tsv
```

### Performance testing:
```bash
python measure-performance.py
```

## Code Overview

### Core Components

- **microsatellite.c**: High-performance C extension implementing the "Brute Force Search" algorithm for microsatellite detection. Searches for perfect repeats of 1-6 nucleotide motifs.

- **microsatnavigator.py**: Main analysis script with command-line interface. Supports both FASTA and FASTQ input, with optional motif standardization.

- **utils.py**: Utility functions for genome processing and microsatellite analysis across different chromosome types.

- **tidyup.py/tidyup-ox.py**: Data organization scripts for processing genome files from public repositories.

### Key Features

- **Fast Algorithm**: Uses brute force search optimized in C for speed
- **Motif Standardization**: Converts microsatellite motifs to canonical forms
- **Genome-wide Analysis**: Processes entire genomes efficiently
- **Multiple Input Formats**: Supports both FASTA and FASTQ files
- **Configurable Parameters**: Adjustable minimum repeat thresholds for different motif lengths

### Default Parameters
- Mononucleotides: ≥12 repeats
- Dinucleotides: ≥7 repeats  
- Tri-, Tetra-, Penta-, Hexanucleotides: ≥4-5 repeats

## Output Format

Results are saved as tab-separated values (TSV) with columns:
- Sequence ID
- Motif sequence
- Motif length
- Number of repeats
- Start position
- End position
- Total length

## References

Rasoarahona, R., Wattanadilokchatkun, P., Panthum, T., Jaisamut, K., Lisachov, A., Thong, T., ... & Srikulnath, K. (2023). MicrosatNavigator: exploring nonrandom distribution and lineage-specificity of microsatellite repeat motifs on vertebrate sex chromosomes across 186 whole genomes. *Chromosome Research*, 31(4), 29. https://doi.org/10.1007/s10577-023-09738-4

## Notes

This tool was developed for analyzing microsatellite distributions in vertebrate sex chromosomes and has been tested on 186 vertebrate genomes. The C implementation provides significant speed improvements over pure Python implementations for large-scale genomic analysis.