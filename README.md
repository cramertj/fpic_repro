# Reproducer for Bazel 7.2.0 fPIC Error

See [this Github issue for more details](https://github.com/bazelbuild/bazel/issues/22932).

The error can be reproduced here with `bazelisk build :server`. It will only occur
when a go_grpc_library is included and referenced.

The error demonstrated here occurs only on Bazel 7.2.0 and later
(specified here in .bazelversion).
