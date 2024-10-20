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
