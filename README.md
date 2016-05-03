# CUDA implementation of the LATCH descriptor & brute-force matcher

This is a high performance GPU implementation of the [LATCH descriptor](http://www.openu.ac.il/home/hassner/projects/LATCH/) invented by [Gil Levi](https://gilscvblog.com/2015/11/07/performance-evaluation-of-binary-descriptor-introducing-the-latch-descriptor/) and [Tal Hassner](http://www.openu.ac.il/home/hassner/). Please reference: "LATCH: Learned Arrangements of Three Patch Codes", IEEE Winter Conference on Applications of Computer Vision (WACV), Lake Placid, NY, USA, March, 2016.

Pull requests (and feature requests!) are encouraged. This repository is under active development.

[![IMAGE ALT TEXT](http://img.youtube.com/vi/zmfLZY7T6Qg/0.jpg)](http://www.youtube.com/watch?v=zmfLZY7T6Qg "Video Title")

On a GTX 970M I see 10^6 descriptor extractions per second, and 3*10^9 comparisons per second. A GTX 760 sees 70% of this speed. NVidia graphics card with CUDA compute capability >=3.0 required.

Look at min.cpp for a minimal introduction. Compile it with "make min -j7". Run it as "./min 1.png 2.png"

vo.cpp has a better example of how you can hide 100% of the processing time of the GPU. The quickest way to see it in action is to install "youtube-dl" and then run "make demo -j7". Or you could just watch this video: https://www.youtube.com/watch?v=zmfLZY7T6Qg I see cumulative 43ms of CPU overhead for GPU processing of 4250 frames of 1080p video.

Note that currently each descriptor is 2048 bits but the last 1536 bits are 0. I was originally planning on building larger variants: true 1024 bit and 2048 bit LATCH descriptors.

Current features:
- hardware interpolation for oriented descriptors at no performance overhead
- arbitrary scaling of region of interest at no performance overhead
- customizable importance masking for patch triplet comparisons at no performance overhead
- asynchronous GPU operation
- fast cross-checking (symmetry test) with event-driven multi-stream matching kernel

Approximate order of upcoming features:
- multichannel support ( http://arxiv.org/abs/1603.04408 )
- extractor kernel granularity optimization (possibly increased extractor speed)
- documentation
- 512 bit matcher (increased matcher speed)
- API improvements (currently a mess)
- CUDA implementation of adaptive grid FAST detector
- offline parameter optimization with PyGMO
- integration into OpenCV

Multi-GPU support is not currently planned. Please contact me if you have a use case that requires it.

This work is released under a Creative Commons Attribution-ShareAlike license. If you use this code in an academic work, please cite me by name (Christopher Parker) and link to this repository.
