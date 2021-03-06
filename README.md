<a href="http://arrayfire.com/"><img src="http://arrayfire.com/logos/arrayfire_logo_whitebkgnd.png" width="300"></a>

ArrayFire is a general-purpose library that simplifies the process of developing
software that targets parallel and massively-parallel architectures including
CPUs, GPUs, and other hardware acceleration devices.

To achieve this goal, ArrayFire provides software developers with a high-level
abstraction of data which resides on the accelerator, the `af::array` object
(or C-style struct).
Developers write code which performs operations on ArrayFire arrays which, in turn,
are automatically translated into near-optimal kernels that execute on the computational
device.
ArrayFire is successfully used on devices ranging from low-power mobile phones to
high-power GPU-enabled supercomputers including CPUs from all major vendors (Intel, AMD, Arm),
GPUs from the dominant manufacturers (NVIDIA, AMD, and Qualcomm), as well as a variety
of other accelerator devices on Windows, Mac, and Linux.

Several of ArrayFire's benefits include:

* [Easy to use](http://arrayfire.org/docs/gettingstarted.htm), stable,
  [well-documented](http://arrayfire.org/docs) API.
* Rigorously Tested for Performance and Accuracy
* Commercially Friendly Open-Source Licensing
* Commercial support from [ArrayFire](http://arrayfire.com)
* [Read about more benefits on Arrayfire.com](http://arrayfire.com/the-arrayfire-library/)

### Build and Test Status

|         | Linux x86_64 | Linux aarch64 | OSX | Windows |
|:-------:|:------------:|:-------------:|:---:|:-------:|
| Build   | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-linux/build/devel)](http://ci.arrayfire.org/job/arrayfire-linux/job/build/job/devel/) | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-tegrax1/build/devel)](http://ci.arrayfire.org/job/arrayfire-tegrax1/job/build/job/devel/) | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-osx/build-mkl/devel)](http://ci.arrayfire.org/job/arrayfire-osx/job/build-mkl/job/devel/) | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-windows/build/devel)](http://ci.arrayfire.org/job/arrayfire-windows/job/build/job/devel/) |
| Test    | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-linux/test/devel)](http://ci.arrayfire.org/job/arrayfire-linux/job/test/job/devel/) | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-tegrax1/test/devel)](http://ci.arrayfire.org/job/arrayfire-tegrax1/job/test/job/devel/) | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-osx/test-mkl/devel)](http://ci.arrayfire.org/job/arrayfire-osx/job/test-mkl/job/devel/) | [![Build Status](http://ci.arrayfire.org/buildStatus/icon?job=arrayfire-windows/test/devel)](http://ci.arrayfire.org/job/arrayfire-windows/job/test/job/devel/) |

### Installation

You can install the ArrayFire library from one of the following ways:

#### Official installers

Execute one of our [official binary installers](https://arrayfire.com/download)
for Linux, OSX, and Windows platforms.

#### Build from source

Build from source by following instructions on our
[wiki](https://github.com/arrayfire/arrayfire/wiki).

### Examples

The following examples are simplified versions of
[`helloworld.cpp`](https://github.com/arrayfire/arrayfire/tree/devel/examples/helloworld/helloworld.cpp)
and
[`conway_pretty.cpp`](https://github.com/arrayfire/arrayfire/tree/devel/examples/graphics/conway_pretty.cpp),
respectively. For more code examples, visit the
[`examples/`](https://github.com/arrayfire/arrayfire/tree/devel/examples)
directory.

#### Hello, world!

```cpp
array A = randu(5, 3, f32); // Create 5x3 matrix of random floats on the GPU
array B = sin(A) + 1.5;     // Element-wise arithmetic
array C = fft(B);           // Fourier transform the result

float d[] = { 1, 2, 3, 4, 5, 6 };
array D(2, 3, d, afHost);   // Create 2x3 matrix from host data
D.col(0) = D.col(end);      // Copy last column onto first

array vals, inds;
sort(vals, inds, A);        // Sort A and print sorted array and corresponding indices
af_print(vals);
af_print(inds);
```

#### Conway's Game of Life

Visit the
[Wikipedia page](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life) for a
description of Conway's Game of Life.

```cpp
static const float h_kernel[] = {1, 1, 1, 1, 0, 1, 1, 1, 1};
static const array kernel(3, 3, h_kernel, afHost);

array state = (randu(128, 128, f32) > 0.5).as(f32); // Generate starting state
Window myWindow(256, 256);
while(!myWindow.close()) {
  array nHood = convolve(state, kernel); // Obtain neighbors
  array C0 = (nHood == 2);               // Generate conditions for life
  array C1 = (nHood == 3);
  state = state * C0 + C1;               // Update state
  myWindow.image(state);                 // Display
}

```

<p align="center">
<img src="https://github.com/arrayfire/assets/blob/master/gifs/conway.gif" alt="Conway's Game of Life" height="256" width="256">
</p>

### Documentation

You can find our complete documentation [here](http://www.arrayfire.com/docs/index.htm).

Quick links:

* [List of functions](http://www.arrayfire.org/docs/group__arrayfire__func.htm)
* [Tutorials](http://www.arrayfire.org/docs/usergroup0.htm)
* [Examples](http://www.arrayfire.org/docs/examples.htm)
* [Blog](http://arrayfire.com/blog/)

### Language wrappers

We currently support the following language wrappers for ArrayFire:

* [`arrayfire-python`](https://github.com/arrayfire/arrayfire-python)
* [`arrayfire-rust`](https://github.com/arrayfire/arrayfire-rust)

Wrappers for other languages are a work in progress:

[`arrayfire-dotnet`](https://github.com/arrayfire/arrayfire-dotnet), [`arrayfire-fortran`](https://github.com/arrayfire/arrayfire-fortran), [`arrayfire-go`](https://github.com/arrayfire/arrayfire-go), [`arrayfire-java`](https://github.com/arrayfire/arrayfire-java), [`arrayfire-lua`](https://github.com/arrayfire/arrayfire-lua), [`arrayfire-nodejs`](https://github.com/arrayfire/arrayfire-js), [`arrayfire-r`](https://github.com/arrayfire/arrayfire-r)

### Contributing

Contributions of any kind are welcome! Please refer to
[CONTRIBUTING.md](https://github.com/arrayfire/arrayfire/blob/master/CONTRIBUTING.md)
to learn more about how you can get involved with ArrayFire.

### Citations and Acknowledgements

If you redistribute ArrayFire, please follow the terms established in
[the license](LICENSE). If you wish to cite ArrayFire in an academic
publication, please use the following [citation document](.github/CITATION.md).

ArrayFire development is funded by ArrayFire LLC and several third parties,
please see the list of [acknowledgements](ACKNOWLEDGEMENTS.md) for further
details.

### Support and Contact Info [![Join the chat at https://gitter.im/arrayfire/arrayfire](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/arrayfire/arrayfire?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

* [Google Groups](https://groups.google.com/forum/#!forum/arrayfire-users)
* ArrayFire Services:  [Consulting](http://arrayfire.com/consulting/)  |  [Support](http://arrayfire.com/support/)   |  [Training](http://arrayfire.com/training/)

### Trademark Policy

The literal mark “ArrayFire” and ArrayFire logos are trademarks of
AccelerEyes LLC DBA ArrayFire.
If you wish to use either of these marks in your own project, please consult
[ArrayFire's Trademark Policy](http://arrayfire.com/trademark-policy/)
