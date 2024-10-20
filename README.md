# Switchyard ⚡️🚋

Bazel build rules for [Yepkit](https://www.yepkit.com/) switchable USB hubs and USB relays using [uhidctl](https://github.com/mvp/uhidctl).

Compiling these tools and installg them and bunding them with test software can be annoying. With these bazel build rules, things get
a bit easier.

## Installation

There are no official releases yet but using a `git_override` this can be used:

```python
bazel_dep(name = "switchyard", version = "0.1")

git_override(
    module_name = "switchyard",
    remote = "https://github.com/sschaetz/switchyard",
    commit = "6fc2c0ca35ad3c73fd003d80b0d3ac03380fbf6d",
)
```

## Usage

When checkout out this repository use the tools like this:

```bash
bazel run //vendor:ykush -- -h
bazel run //vendor:uhidctl -- -h
```

Through bzlmod use the tools like this:

```bash
bazel run @switchyard//vendor:ykush -- -h
bazel run @switchyard//vendor:uhidctl -- -h
```

And of course they can be added as tools to other targets.
