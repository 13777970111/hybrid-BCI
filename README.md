# hybrid-BCI
Tutorial for data processing for hybrid BCI

The authors would be grateful if published reports of research using this code (or a modified version, maintaining a significant portion of the original code) would cite the following article:

Shin, Jaeyoung, et al. "Open Access Dataset for EEG+ NIRS Single-Trial Classification." IEEE Transactions on Neural Systems and Rehabilitation Engineering (2016), DOI: 10.1109/TNSRE.2016.2628057.

# Basic Data Structures of the BBCI Toolbox 
This document is from https://github.com/bbci/bbci_public/blob/master/doc/ToolboxData.markdown and partly modified.
For more details, visit BBCI toolbox.


## Table of Contents

- [`cnt`](#Cnt) - _Data structure holding the continuous signals_
- [`mrk`](#Mrk) - _Marker structure defining certain events_
- [`mnt`](#Mnt) - _Montage structure defining the electrode layout for scalp and grid plots_

## `cnt` - Continuous signals (EEG) <a id="Cnt"></a>

The structure holding continuous (i.e., not epoched) EEG signals is denoted by `cnt`.

**`cnt`** | **is a structure with the following fields:**
--------- | ---------------------------------------------
`.clab`   |   channel labels (`CELL {1 #channels}`) there may be additional information in other fields, but these are all optional
`.fs`     |   sampling rate [samples per second]
`.title`  |   task type: 'MI' - motor imagery / 'MA' - mental arithmetic
`.T`      |   length of cnt.x
`.yUnit`  |   unit of cnt.x
`.x`      |   multichannel signals (`DOUBLE [T #channels]`)

## `mrk` - Event markers   <a id="Mrk"></a>

The structure holding marker (or event) information is denoted by `mrk`. Using
this structure you can segment continuous EEG signals into epochs by the
function `proc_segmentation`.

**`mrk`**    | **is a structure with the following fields:**
------------ | ---------------------------------------------
`.time`      | defines the time points of events in msec (`DOUBLE [1 #events]`)
`.event.desc`| structure of further information; each field of `mrk.event` provides information that is specified for each event, given in arrays that index the events _in their first dimension_. This is required such that functions like `mrk_selectEvents` can work properly on those variables.
`.y`         | class labels (`DOUBLE [#classes #events]`)
`.className` | class names (`CELL {1 #classes}`)

## `mnt` - The electrode montage   <a id="Mnt"></a>

The electrode montage structure, denoted by `mnt`, holds the information of the
spatial arrangement of the electrodes on the scalp (for plotting scalp
topographies) and the arrangement of subplot axes for multi-channel plots.

**`mnt`**       | **is a structure with the following fields:**
--------------- | ---------------------------------------------
`.clab`         | channel labels (`CELL {1 #channels}`)
`.x`            | x-position of the electrode for scalp maps (`DOUBLE [1 +channels]`)
`.y`            | y-position of the electrode for scalp maps (`DOUBLE [1 +channels]`)
                | **further optional fields are required for multichannel plots:**
`.box`          | positions of subplot axes for multichannel plots (`DOUBLE [2 #channels]` or `[2 #channels+1]`; the first row holds the horizontal, and the second row the vertical positions. The optional last column specifies the position of the legend
`.box_sz`       | size of subplot axes for multichannel plots (`DOUBLE [2 #channels]` or `[2 #nchannels+1]`), corresponding to `.box`. The first row holds the width, the second row the height
`.scale_box`    | position of subplot for the scale (`DOUBLE [2 1]`)
`.scale_box_sz` | size of subplot for the scale (`DOUBLE [2 1]`)
