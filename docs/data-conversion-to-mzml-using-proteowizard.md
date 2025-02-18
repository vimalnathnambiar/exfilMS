# Data Conversion to mzML using ProteoWizard

### Table of Contents

1. [Introduction](#introduction)

2. [Supported Vendor Formats](#supported-vendor-formats)

3. [Installation](#installation)

   - [Graphical User Interface](#method-1---graphical-user-interface-windows)
   - [Docker](#method-2---via-docker)

4. [Usage](#usage)

   - [Graphical User Interface](#method-1---graphical-user-interface-windows-1)
   - [Docker](#method-2---via-docker-1)

<br>

## Introduction

Data retrieved from MS instruments (from now on referred to as raw MS data) is widely stored in proprietary vendor formats that are optimised to its respective hardware and are only accessibly using vendor-provided software libraries. To enable cross-platform data integration and analysis, mzML was introduced as an open, universal format to store raw MS data acquired independently of vendor-specific instruments. One of the most prominent way of converting these raw MS data files to mzML is using the ProteoWizard _msConvert_ tool.

<br>

## Supported Vendor Formats

The following formats are currently supported by ProteoWizard _msConvert_ for data conversion:

| Format                  | Status      |
| ----------------------- | ----------- |
| ABI T2D                 | Not working |
| Agilent MHDAC (non-IMS) | Working     |
| Agilent MHDAC (IMS)     | Working     |
| Bruker BAF              | Working     |
| Bruker FID/YEP          | Not Working |
| Bruker TDF              | Working     |
| SCIEX WIFF              | Working     |
| SCIEX WIFF2             | Working     |
| Shimadzu QQQ            | Working     |
| Shimadzu QToF           | Working     |
| Thermo RAW              | Working     |
| Waters RAW              | Working     |
| Waters UNIFI            | Not Working |

<br>

## Installation

### Method 1 - Graphical User Interface (Windows)

Download [ProteoWizard][pwiz-download]

<br>

### Method 2 - via Docker

Download [Docker][docker-url]

> [!NOTE]\
> If you are using Linux, it is recommended to download the Docker Engine.

<br>

## Usage

### Method 1 - Graphical User Interface (Windows)

1. Launch `msConvertGUI`

2. Choose your raw MS data files to be converted

3. Configure the conversion parameters

4. Begin conversion

<br>

### Method 2 - via Docker

1. Launch `Docker`

   If you are using Docker Engine, execute one of the following from your terminal.

   ```md
   # To start Docker manually

   sudo systemctl start docker
   ```

   or

   ```md
   # To configure Docker to start on boot with systemd

   sudo groupadd docker
   sudo usermod -aG docker <username>

   sudo systemctl enable docker.service
   sudo systemctl enable containerd.service
   ```

   > _Please log out and log back into your device for membership re-evaluation. Restart may be required._

<br>

2. Execute docker command from terminal

   ```md
   # Run ProteoWizard msConvert with default data conversion parameters

   docker run --rm -v "/path/to/directory/containing/raw/MS/data/":/inputDirectory -v "/path/to/output/directory/":/outputDirectory proteowizard/pwiz-skyline-i-agree-to-the-vendor-licenses wine msconvert /inputDirectory/"*.*" -o /outputDirectory

   # Default data conversion parameters used

   format: mzML
      m/z: Compression-None, 64-bit
      intensity: Compression-None, 32-bit
      rt: Compression-None, 64-bit
   ByteOrder_LittleEndian
      indexed="true"
   outputPath: /outputDirectory
   extension: .mzML
   contactFilename:
   runIndexSet:

   spectrum list filters:

   chromatogram list filters:

   filenames:
   ```

   For more info on all available conversion parameters provided by ProteoWizard _msConvert_ tool, please refer [here][msconvert-doc].

<!-- URLs used in the markdown document -->

[pwiz-download]: https://proteowizard.sourceforge.io/download.html
[docker-url]: https://docs.docker.com/engine/install/
[msconvert-doc]: https://proteowizard.sourceforge.io/tools/msconvert.html
