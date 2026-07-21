# YoloObjectDetection

The name doesn't match what's actually in this repo: the notebook here
uses [Mask R-CNN](https://github.com/matterport/Mask_RCNN) — a different
image-recognition model, not YOLO — to detect and outline objects in
images using weights already trained on a large public image dataset
(COCO). I'm not renaming the repo, but it's worth saying plainly up front
rather than letting the mismatch stand unexplained.

## This one can't be re-run or re-verified

Two separate problems here, not one:

- It depends on specific old versions of TensorFlow and Keras (two widely
  used machine-learning libraries), plus a copy of the Mask R-CNN project
  that hasn't been updated to work with newer versions of those libraries
  in years. Getting this exact combination running on a current computer
  is its own significant undertaking, separate from anything in this
  notebook itself.
- Even setting that aside, the notebook as written is missing a step. The
  cell that's supposed to load the pretrained weights refers to a model
  object and a file path that are never actually created anywhere earlier
  in the notebook. The step that would normally build the model and
  specify where to find the weights simply isn't there. This isn't a
  compatibility problem — the notebook wouldn't run start to finish even
  in exactly the right setup.

I didn't try to write in that missing step myself. The standard code for
it exists in Mask R-CNN's own example notebooks, but adding code here that
I can't actually run and check would just be a different way of guessing,
dressed up as a fix.

## What got fixed

- **A repeated setup step that would fail on a second run.** The notebook
  downloaded the Mask R-CNN project twice — once with a check for whether
  it was already present, and then again unconditionally right after,
  regardless of that check. The second download would error out on any
  run after the first one. Removed.

## Running it

You'd need: the specific old versions of TensorFlow and Keras this
notebook was built with, a working copy of the Mask R-CNN project, the
pretrained COCO weights file, and the missing model-setup step described
above filled in yourself.
