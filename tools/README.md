# LIF data tools

> **Draft written from the code; to be checked by the unit's staff.**

Two small Python scripts for Leica `.lif` project files, the format the Stellaris (and SP8) confocal software saves. Both are run from a terminal and ask for their inputs; neither changes the `.lif` file.

| Script | What it does | Status |
|---|---|---|
| [`lif-reader.py`](lif-reader.py) | Lists the images in a `.lif` file with their dimensions | Working (untested here) |
| [`WIP_leica_lif_processor.py`](WIP_leica_lif_processor.py) | Saves each image of a `.lif` file as an OME-TIFF, optionally as a projection | Work in progress (see the limits below) |

## Requirements

- Python 3
- [`readlif`](https://pypi.org/project/readlif/) (both scripts)
- `numpy` and [`aicsimageio`](https://pypi.org/project/aicsimageio/) (its `OmeTiffWriter`; only `WIP_leica_lif_processor.py`)

```bash
pip install readlif numpy aicsimageio
```

## lif-reader.py: list the images in a `.lif` file

```bash
python lif-reader.py
```

It asks for the full path to the `.lif` file, including the file name. Quotes around the path, as Windows adds when you use "Copy as path", are removed. For each image (series) in the file it prints:

- the image name
- its dimensions, as reported by `readlif` (x, y, z, t, mosaic tiles)
- the number of Z frames
- the number of T (time) frames
- the number of channels

If the path does not exist it prints `File not found!`; if the file cannot be read it prints the error. Nothing is written to disk.

## WIP_leica_lif_processor.py: save images as OME-TIFF

```bash
python WIP_leica_lif_processor.py
```

It asks for:

1. the full path to the `.lif` file;
2. the output folder (it must already exist; the script does not create it);
3. the projection type: `Max`, `Average`, `Sum` or `None`.

For every image in the file it writes `<image name>.ome.tiff` into the output folder:

- `Max`, `Average`, `Sum`: one 2D image, the maximum, mean or sum of the frames, saved with dimension order `YX`. `Average` and `Sum` change the pixel type (float / 64-bit integer); `Max` keeps it.
- `None`: all frames as a stack, saved with dimension order `ZYX`.

**Limits of the current version** (why it is marked work in progress):

- **Only time frames are processed.** The frames come from `readlif`'s `get_iter_t()` with its defaults, i.e. the time series of the **first channel at the first Z position** (and the first tile of a mosaic). Z-stacks are not projected, and the other channels are not saved. For a single time point the "projection" is just that one plane.
- With `None`, a time series is written with its time axis labelled as Z (`ZYX`).
- The projection type is read with `.capitalize()`, so typing "Standard Deviation" becomes "Standard deviation", which the script does not accept (it stops with `Unknown projection type`). The standard deviation option in the code therefore cannot be chosen at the prompt.
- The image name from the `.lif` file is used as the file name unchanged; a name containing `/` would point into a sub-folder, which must exist.
- If `readlif` cannot read the file it prints the error and `Failed to load dataset.`, and nothing is written. Errors while writing are not caught.
- Large files need enough RAM for all images at once: every image is loaded before the first one is written.
