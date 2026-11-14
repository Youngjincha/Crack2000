crops_2000: the frozen crop set used for SDDNet and STRNet training and testing

2,000 crops of 1024 x 512 px (width x height), cut from the STRNet dataset
(Kang & Cha 2022): 1,740 images after 8 duplicates were removed.

  train/images, train/masks   1,500 pairs (from 1,240 source images)
  test/images,  test/masks      500 pairs (from 500 source images)

An image and its mask have the same filename.

Split: by source image. Every crop of one image is on the same side, and no
source image appears in both train and test. The 84 overlapping extra crops
and the 25 crops with no crack are all in train.

Masks are stored as RGB. Crack = luma > 127, e.g. in Python:
  Image.open(mask).convert("L") > 127
A few masks have soft (anti-aliased) crack edges; these come from the
original STRNet annotation. One test image is stored RGBA; read images with
.convert("RGB").

manifest.csv, one row per crop:
  crop       crop filename
  split      train / test (this set)
  src_split  the source image's original STRNet split
  src        source image filename
  rotated    1 = portrait image rotated to landscape before cropping
  y, x       crop offset in the (rotated) source image, px
  extra      1 = one of the 84 overlapping extra crops
  crack_px   crack pixels in the crop

The crops hold 92.56% of the annotated crack pixels of the source images.
