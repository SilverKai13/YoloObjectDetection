# YoloObjectDetection

The name doesn't match the content: this notebook uses
[matterport/Mask_RCNN](https://github.com/matterport/Mask_RCNN) —
Mask R-CNN, not YOLO — to run instance segmentation on images using
COCO pretrained weights. Not renaming the repo, but worth saying
plainly up front rather than letting the mismatch stand unexplained.

## This one can't be re-run or re-verified

Two separate problems, not one:

- It installs `tensorflow==1.13.1` and `keras==2.1.0`, and clones
  `matterport/Mask_RCNN`, which hasn't been updated for TF2 and is
  effectively unmaintained. Getting this combination installed on
  anything current is its own project, separate from anything in this
  notebook.
- Even granting a working legacy environment, the notebook as
  committed is missing a step: the "load pretrained weights" cell
  calls `model.load_weights(COCO_MODEL_PATH, by_name=True)`, but
  neither `model` nor `COCO_MODEL_PATH` is ever defined anywhere
  above it. The cell that would normally build the inference model
  (`modellib.MaskRCNN(mode="inference", ...)`) and set the weights
  path isn't here. This isn't a version-compatibility issue — the
  notebook wouldn't run top to bottom even in the exact right
  environment.

I didn't try to write that missing cell in. The standard boilerplate
for it exists in matterport's own demo notebooks, but adding code I
can't run and verify here would just be a different way of guessing,
dressed up as a fix.

## What got fixed

- **A redundant `git clone`.** The notebook cloned
  `matterport/Mask_RCNN` twice: once conditionally (only if the
  directory doesn't already exist), and then again unconditionally
  right after. The second clone would error on any run after the
  first. Removed.

## Running it

You'd need: TensorFlow 1.13.1, Keras 2.1.0, a working
`matterport/Mask_RCNN` checkout, COCO pretrained weights
(`mask_rcnn_coco.h5`), and the missing model-instantiation cell
described above filled in.
