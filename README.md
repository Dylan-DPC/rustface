<h1 align="center">
    <a href="http://atomashpolskiy.github.io/rustface/">Rustface</a>
</h1>

<p align="center"><strong>
<sup>
<br/><a href="https://github.com/seetaface/SeetaFaceEngine/tree/master/FaceDetection">SeetaFace Detection</a> in Rust programming language
</sup>
</strong></p>

<p align="center">
    <img src="https://atomashpolskiy.github.io/static/img/scientists.png" alt="Bt Example">
</p>

<p align="left">
    <a href="https://opensource.org/licenses/BSD-2-Clause">
        <img src="https://img.shields.io/badge/license-BSD-blue.svg"
             alt="License">
    </a>
</p>

## About

SeetaFace Detection is an implementation of Funnel-Structured cascade, which is designed for real-time multi-view face detection. FuSt aims at a good trade-off between accuracy and speed by using a coarse-to-fine structure. It consists of multiple view-specific fast LAB cascade classifiers at early stages, followed by coarse Multilayer Perceptron (MLP) cascades at later stages. The final stage is one unified fine MLP cascade, processing all proposed windows in a centralized style. 

[Read more...](https://github.com/seetaface/SeetaFaceEngine/tree/master/FaceDetection)

## Usage example

```rust
extern crate rustface;

use rustface::{Detector, FaceInfo, ImageData};

fn main() {
    let mut detector = rustface::create_detector("/path/to/model").unwrap();
    detector.set_min_face_size(20);
    detector.set_score_thresh(2.0);
    detector.set_pyramid_scale_factor(0.8);
    detector.set_slide_window_step(4, 4);
    
    let mut image = ImageData::new(bytes, width, height);
    for face in detector.detect(&mut image).into_iter() {
        // print confidence score and coordinates
        println!("found face: {:?}", face);
    }
}
```

## How to build

The project is a library crate, but also contains a runnable module for demonstration purposes. In order to build it, you'll need an OpenCV 2.4 installation for [generation of Rust bindings](https://github.com/kali/opencv-rust).

Otherwise, the project relies on the stable Rust toolchain, so just use the standard Cargo `build` command:

```
cargo build --release
```

## Run demo

Code for the demo is located in `main.rs` file. It performs face detection for the given image and opens it in a separate window.

```
$ cargo run --release model/seeta_fd_frontal_v1.0.bin <path-to-image>
```

## TODO

* Use SSE for certain transformations in `math` module and `SurfMlpFeatureMap`
* Use OpenMP for parallelization of some CPU intensive loops
* Tests (it would make sense to start with an integration test for `Detector::detect`, based on the results retrieved from the original library)

## License

Original SeetaFace Detection is released under the [BSD 2-Clause license](https://github.com/seetaface/SeetaFaceEngine/blob/master/LICENSE). This project is a derivative work and uses the same license as the original.