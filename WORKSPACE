# Copyright 2021 The Pigweed Authors
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may not
# use this file except in compliance with the License. You may obtain a copy of
# the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
# License for the specific language governing permissions and limitations under
# the License.

workspace(
    name = "pigweed",
)

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository", "new_git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
# load(
#     "//pw_env_setup/bazel/cipd_setup:cipd_rules.bzl",
#     "cipd_client_repository",
#     "cipd_repository",
# )

# Set up Bazel platforms.
# Required by: pigweed.
# Used in modules: //pw_build, (Assorted modules via select statements).
http_archive(
    name = "platforms",
    sha256 = "8150406605389ececb6da07cbcb509d5637a3ab9a24bc69b1101531367d89d74",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/platforms/releases/download/0.0.8/platforms-0.0.8.tar.gz",
        "https://github.com/bazelbuild/platforms/releases/download/0.0.8/platforms-0.0.8.tar.gz",
    ],
)

http_archive(
    name = "rules_platform",
    sha256 = "0aadd1bd350091aa1f9b6f2fbcac8cd98201476289454e475b28801ecf85d3fd",
    urls = [
        "https://github.com/bazelbuild/rules_platform/releases/download/0.1.0/rules_platform-0.1.0.tar.gz",
    ],
)

http_archive(
    name = "rules_cc",
    sha256 = "2037875b9a4456dce4a79d112a8ae885bbc4aad968e6587dca6e64f3a0900cdf",
    strip_prefix = "rules_cc-0.0.9",
    urls = ["https://github.com/bazelbuild/rules_cc/releases/download/0.0.9/rules_cc-0.0.9.tar.gz"],
)

# local_repository(
#     name = "pw_toolchain",
#     path = "pw_toolchain_bazel",
# )
# 
# # Setup CIPD client and packages.
# # Required by: pigweed.
# # Used by modules: all.
# cipd_client_repository()
# 
# load("//pw_toolchain:register_toolchains.bzl", "register_pigweed_cxx_toolchains")
# 
# register_pigweed_cxx_toolchains()

# Set up Starlark library.
# Required by: io_bazel_rules_go, com_google_protobuf, rules_python
# Used in modules: None.
# This must be instantiated before com_google_protobuf as protobuf_deps() pulls
# in an older version of bazel_skylib. However io_bazel_rules_go requires a
# newer version.
http_archive(
    name = "bazel_skylib",  # 2022-09-01
    sha256 = "4756ab3ec46d94d99e5ed685d2d24aece484015e45af303eb3a11cab3cdc2e71",
    strip_prefix = "bazel-skylib-1.3.0",
    urls = ["https://github.com/bazelbuild/bazel-skylib/archive/refs/tags/1.3.0.zip"],
)

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

# Used in modules: //pw_grpc
#
# TODO: b/345806988 - remove this fork and update to upstream HEAD.
git_repository(
    name = "io_bazel_rules_go",
    commit = "21005c4056de3283553c015c172001229ecbaca9",
    remote = "https://github.com/cramertj/rules_go.git",
)

# Used in modules: //pw_grpc
http_archive(
    name = "bazel_gazelle",
    sha256 = "32938bda16e6700063035479063d9d24c60eda8d79fd4739563f50d331cb3209",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.35.0/bazel-gazelle-v0.35.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.35.0/bazel-gazelle-v0.35.0.tar.gz",
    ],
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.21.5")

gazelle_dependencies()

# load("//pw_grpc:deps.bzl", "pw_grpc_deps")
# 
# # gazelle:repository_macro pw_grpc/deps.bzl%pw_grpc_deps
# pw_grpc_deps()

http_archive(
    name = "rules_proto",
    sha256 = "dc3fb206a2cb3441b485eb1e423165b231235a1ea9b031b4433cf7bc1fa460dd",
    strip_prefix = "rules_proto-5.3.0-21.7",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/5.3.0-21.7.tar.gz",
    ],
)


# Set up Protobuf rules.
# Required by: pigweed.
# Used in modules: //pw_protobuf.
# TODO: pwbug.dev/319717451 - Keep this in sync with the pip requirements.
http_archive(
    name = "com_google_protobuf",
    sha256 = "616bb3536ac1fff3fb1a141450fa28b875e985712170ea7f1bfe5e5fc41e2cd8",
    strip_prefix = "protobuf-24.4",
    url = "https://github.com/protocolbuffers/protobuf/releases/download/v24.4/protobuf-24.4.tar.gz",
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()




# # Setup Fuchsia SDK.
# # Required by: bt-host.
# # Used in modules: //pw_bluetooth_sapphire.
# # NOTE: These blocks cannot feasibly be moved into a macro.
# # See https://github.com/bazelbuild/bazel/issues/1550
# git_repository(
#     name = "fuchsia_infra",
#     # ROLL: Warning: this entry is automatically updated.
#     # ROLL: Last updated 2024-06-08.
#     # ROLL: By https://cr-buildbucket.appspot.com/build/8745662233558600481.
#     commit = "5084a6ded7858e2824e9a683d5ca33745140723b",
#     remote = "https://fuchsia.googlesource.com/fuchsia-infra-bazel-rules",
# )
# 
# load("@fuchsia_infra//:workspace.bzl", "fuchsia_infra_workspace")
# 
# fuchsia_infra_workspace()
# 
# FUCHSIA_SDK_VERSION = "version:20.20240408.3.1"
# 
# cipd_repository(
#     name = "fuchsia_sdk",
#     path = "fuchsia/sdk/core/fuchsia-bazel-rules/${os}-amd64",
#     tag = FUCHSIA_SDK_VERSION,
# )
# 
# load("@fuchsia_sdk//fuchsia:deps.bzl", "rules_fuchsia_deps")
# 
# rules_fuchsia_deps()
# 
# register_toolchains("@fuchsia_sdk//:fuchsia_toolchain_sdk")
# 
# cipd_repository(
#     name = "fuchsia_products_metadata",
#     path = "fuchsia/development/product_bundles/v2",
#     tag = FUCHSIA_SDK_VERSION,
# )
# 
# load("@fuchsia_sdk//fuchsia:products.bzl", "fuchsia_products_repository")
# 
# fuchsia_products_repository(
#     name = "fuchsia_products",
#     metadata_file = "@fuchsia_products_metadata//:product_bundles.json",
# )
# 
# load("@fuchsia_sdk//fuchsia:clang.bzl", "fuchsia_clang_repository")
# 
# fuchsia_clang_repository(
#     name = "fuchsia_clang",
#     # TODO: https://pwbug.dev/346354914 - Reuse @llvm_toolchain. This currently
#     # leads to flaky loading phase errors!
#     # from_workspace = "@llvm_toolchain//:BUILD",
#     cipd_tag = "git_revision:c58bc24fcf678c55b0bf522be89eff070507a005",
#     sdk_root_label = "@fuchsia_sdk",
# )
# 
# load("@fuchsia_clang//:defs.bzl", "register_clang_toolchains")
# 
# register_clang_toolchains()
# 
# # Since Fuchsia doesn't release arm64 SDKs, use this to gate Fuchsia targets.
# load("//pw_env_setup:bazel/host_metadata_repository.bzl", "host_metadata_repository")
# 
# # Registers platforms for use with toolchain resolution
# register_execution_platforms("@local_config_platform//:host", "//pw_build/platforms:all")
