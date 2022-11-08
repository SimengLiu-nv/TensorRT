workspace(name = "Torch-TensorRT")
 
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
 
http_archive(
    name = "rules_python",
    sha256 = "778197e26c5fbeb07ac2a2c5ae405b30f6cb7ad1f5510ea6fdac03bded96cc6f",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.2.0/rules_python-0.2.0.tar.gz",
)
 
load("@rules_python//python:pip.bzl", "pip_install")
 
http_archive(
    name = "rules_pkg",
    sha256 = "038f1caa773a7e35b3663865ffb003169c6a71dc995e39bf4815792f385d837d",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_pkg/releases/download/0.4.0/rules_pkg-0.4.0.tar.gz",
        "https://github.com/bazelbuild/rules_pkg/releases/download/0.4.0/rules_pkg-0.4.0.tar.gz",
    ],
)
 
load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
 
rules_pkg_dependencies()
 
git_repository(
    name = "googletest",
    commit = "703bd9caab50b139428cea1aaff9974ebee5742e",
    remote = "https://github.com/google/googletest",
    shallow_since = "1570114335 -0400",
)
 
# External dependency for torch_tensorrt if you already have precompiled binaries.
local_repository(
    name = "torch_tensorrt",
    path = "/home/simengl/storage/.cache-main-native-x86_64-ubuntu22.04-cuda11.8/turtle/test_venv/lib/python3.10/site-packages/torch_tensorrt",
)
 
# CUDA should be installed on the system locally
new_local_repository(
    name = "cuda",
    build_file = "@//third_party/cuda:BUILD",
    path = "/usr/local/cuda-11.8/",
)
 
new_local_repository(
    name = "cublas",
    build_file = "@//third_party/cublas:BUILD",
    path = "/usr",
)
#############################################################################################################
# Tarballs and fetched dependencies (default - use in cases when building from precompiled bin and tarballs)
#############################################################################################################
 
http_archive(
    name = "libtorch",
    build_file = "@//third_party/libtorch:BUILD",
    strip_prefix = "libtorch",
    urls = ["https://download.pytorch.org/libtorch/nightly/cu117/libtorch-cxx11-abi-shared-with-deps-1.13.0.dev20220921%2Bcu117.zip"],
)
 
http_archive(
    name = "libtorch_pre_cxx11_abi",
    build_file = "@//third_party/libtorch:BUILD",
    strip_prefix = "libtorch",
    urls = ["https://download.pytorch.org/libtorch/nightly/cu117/libtorch-shared-with-deps-1.13.0.dev20220921%2Bcu117.zip"],
)
 
new_local_repository(
   name = "cudnn",
   path = "/externals/cudnn/x86_64/8.8/cuda-11.8/",
   build_file = "@//third_party/cudnn/archive:BUILD"
)
 
new_local_repository(
  name = "tensorrt",
  path = "/home/simengl/trt/build/x86_64-gnu/debug/",
  build_file = "@//third_party/tensorrt/archive:BUILD"
)
 
#########################################################################
# Development Dependencies (optional - comment out on aarch64)
#########################################################################
 
pip_install(
    name = "devtools_deps",
    requirements = "//:requirements-dev.txt",
)