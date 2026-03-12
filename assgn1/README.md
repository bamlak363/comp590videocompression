## Approach

Essentially we have each pixel encoded one at a time with arithmetic encoding. The predictor uses the pixel at the same position in the frame previous, and then goes ahead and encodes the diff. I'm using 256 contexts, one per possible prior pixel value (0-255). This is so that each brightness level has its own probability model for the difference. This means that the regions more stationary always have a diff of 0, so the model learns to assign fewer bits. Which gives better compression than a single global model.

## Results

### bourne.mp4
- Frames encoded: 10
- Compression ratio: 2.74x

### nature.mp4 (nature video)
- Frames encoded: 50 (skipped the first 30 frames to avoid the title card)
- Compression ratio: 10.10x

The difference in ratios is reflective of the type of content, action footage has lots motion and scene cuts which cause large pixel differences between frames, while the nature footage that I added has mostly slow movements and big static regions that compress much better.