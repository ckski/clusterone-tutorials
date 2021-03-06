# TensorBoard Tutorial

<p align="center">
<img src="../co_logo.png" alt="Clusterone" width="200">
<br>
<br>
<a href="https://slackin-altdyjrdgq.now.sh"><img src="https://slackin-altdyjrdgq.now.sh/badge.svg" alt="join us on slack"></a>
</p>

This is a tutorial on how to use [TensorBoard](https://github.com/tensorflow/tensorboard), TensorFlow's visualization suite. The code uses [TensorFlow](https://tensorflow.org) and the [MNIST](http://yann.lecun.com/exdb/mnist/) dataset.

The tutorial is separated into parts. Part 1 introduces graphs, scalar plots, and histograms. Part 2 focuses on outputting images to TensorBoard.

These links get you to the tutorials on the Clusterone blog:

- [Part 1: Graphs, Scalars, and Histograms](https://clusterone.com/blog/2018/04/25/guide-tensorboard-graph-scalar-histogram/)
- [Part 2: Images](https://clusterone.com/blog/2018/04/30/guide-effectively-using-tensorboard-part-2-images/)

Follow the instructions below to run the tutorial code locally and on Clusterone. 

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [More Info](#more-info)
- [License](#license)

## Install

To run the code, you need:

- [Python](https://python.org/) 3.5
- [Git](https://git-scm.com/)
- TensorFlow 1.5. Install it like this: `pip install tensorflow`
- The Clusterone Python library. Install it with `pip install clusterone`
- To run the code on Clusterone, you need a Clusterone account. [Join the waitlist](https://clusterone.com/join-waitlist/) here.

For part 2 of the tutorial, you also need the following Python packages:
- [OpenCV](https://opencv.org/). Install it with `pip install opencv-python`
- [Numpy](http://www.numpy.org/). Get it using `pip install numpy`

### Setting Up

All you need to do is to clone this repository onto your local machine:

```shell
git clone https://github.com/clusterone/clusterone-tutorials
```

## Usage

The tutorial code is divided into multiple stand-alone files.

Part 1:

- [main_bare.py](code/part_1/main_bare.py): A simple implementation of MNIST handwritten digit recognition. This file doesn't contain any visualization with TensorBoard and serves as the starting point for the tutorial.
- [main_tensorboard_graph.py](code/part_1/main_tensorboard_graph.py): Adds names and `tf.name_scope` to the code to produce a network graph in TensorBoard.
- [main_tensorboard.py](code/part_1/main_tensorboard.py): Extends main_tensorboard_graph to include scalar plots using `tf.summary`, as well as histograms.

Part 2:

- [main_tensorboard_images.py](code/part_2/main_tensorboard_images.py): Includes images of misclassified MNIST digits in TensorBoard.

You can run the code on your local machine, as well as on Clusterone without changing the code.

### Run the code locally

Navigate into the directory for [part 1](code/part_1/) or [part 2](code/part_2/) of the tutorial. Assuming all packages are installed correctly, you can run all script with `python <script-name>`. The script will print the necessary command to launch TensorBoard to the console.

### Run on Clusterone

These instructions use the `just` command line tool. It comes with the Clusterone Python library and is installed automatically with the library.

cd into the [part 1](code/part_1/) or [part 2](code/part_2) folder and log into your Clusterone account using `just login`.

First, create a new git repository in the code directory and commit the Python files to it:

```shell
git init
git add .
git commit -m "Initial commit"
```

Then, create a new project on Clusterone:

```shell
just init project tensorboard
```

Now, upload the code to the new project:

```shell
git push clusterone master
```

Finally, create a job. Note that `<MODULE-NAME>` is the name of the Python file. Depending on which file you want to run, this can be `main_tensorboard`, `main_tensorboard_images`, and so on.

```shell
just create job single --project tensorboard --module <MODULE-NAME> --name tb-job --python-version 3 --keeplogs "" --time-limit 1h
```

Now all that's left to do is starting the job:

```shell
just start job -p tensorboard/tb-job
```

That's it! You can monitor its progress on the command line using `just get events`. More elaborate monitoring is available on the [Matrix](https://clusterone.com/matrix), Clusterone's graphical web interface.

## More Info

To learn more about this tutorial, take a look at the corresponding articles on our [blog](https://clusterone.com/blog/tutorials/)!

For further info on the MNIST dataset, check out [Yann LeCun's page](http://yann.lecun.com/exdb/mnist/) about it. To learn more about TensorFlow and Deep Learning in general, take a look at the [TensorFlow](https://tensorflow.org) website.

## License

[MIT](LICENSE) © Clusterone Inc.

The [MNIST](http://yann.lecun.com/exdb/mnist/) dataset has been created and curated by Corinna Cortes, Christopher J.C. Burges, and Yann LeCun.
