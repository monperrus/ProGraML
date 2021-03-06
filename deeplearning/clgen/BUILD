# This package contains CLgen, a deep learning program generator.
#
# CLgen is an open source application for generating runnable programs using
# deep learning. CLgen learns to program using neural networks which model the
# semantics and usage from large volumes of program fragments, generating
# executable programs that are representative of, but distinct from,
# the programs it learns from.
#
# Copyright (c) 2016, 2017, 2018, 2019 Chris Cummins.
#
# clgen is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# clgen is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with clgen.  If not, see <https://www.gnu.org/licenses/>.

load("//tools/bzl:exports.bzl", "exports_repo")

licenses(["restricted"])  # GPL v3

exports_files([
    "LICENSE",
    "README.md",
])

exports_repo(
    name = "export",
    github_repo = "clgen",
    move_file_mapping = {
        "deeplearning/clgen/README.md": "README.md",
        "deeplearning/clgen/LICENSE": "LICENSE",
        "deeplearning/clgen/travis.yml": ".travis.yml",
    },
    targets = [
        "//deeplearning/clgen",
        "tests(//deeplearning/clgen/...)",
    ],
)

py_library(
    name = "cache",
    srcs = ["cache.py"],
    visibility = ["//deeplearning/clgen:__subpackages__"],
    deps = [
        "//labm8/py:app",
        "//labm8/py:cache",
        "//labm8/py:fs",
    ],
)

py_binary(
    name = "clgen",
    srcs = ["clgen.py"],
    visibility = ["//visibility:public"],
    deps = [
        ":errors",
        ":sample_observers",
        ":samplers",
        "//deeplearning/clgen/dashboard",
        "//deeplearning/clgen/models",
        "//deeplearning/clgen/models:pretrained",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:pbutil",
        "//labm8/py:prof",
    ],
)

py_test(
    name = "clgen_test",
    size = "enormous",
    srcs = ["clgen_test.py"],
    data = [
        "//deeplearning/clgen/tests/data:pico",
        "//deeplearning/clgen/tests/data:tiny",
        "//deeplearning/clgen/tests/data/tiny",
    ],
    deps = [
        ":clgen",
        "//deeplearning/clgen:conftest",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:fs",
        "//labm8/py:pbutil",
        "//labm8/py:tar",
        "//labm8/py:test",
    ],
)

py_library(
    name = "conftest",
    testonly = True,
    srcs = ["conftest.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:pbutil",
        "//labm8/py:test",
    ],
)

py_library(
    name = "errors",
    srcs = ["errors.py"],
    visibility = ["//deeplearning/clgen:__subpackages__"],
)

py_binary(
    name = "ls_models",
    srcs = ["ls_models.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//deeplearning/clgen/models",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:pbutil",
    ],
)

py_binary(
    name = "preprocess",
    srcs = ["preprocess.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//deeplearning/clgen/corpuses:preprocessed",
        "//deeplearning/clgen/preprocessors",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:humanize",
        "//third_party/py/progressbar",
    ],
)

py_test(
    name = "preprocess_test",
    srcs = ["preprocess_test.py"],
    deps = [
        ":preprocess",
        "//labm8/py:test",
        "//third_party/py/pytest",
    ],
)

py_library(
    name = "sample",
    srcs = ["sample.py"],
    visibility = ["//visibility:public"],
    deps = [
        ":errors",
        ":samplers",
        "//deeplearning/clgen/models:pretrained",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:pbutil",
    ],
)

py_library(
    name = "sample_observers",
    srcs = ["sample_observers.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:crypto",
        "//labm8/py:fs",
        "//labm8/py:pbutil",
    ],
)

py_test(
    name = "sample_observers_test",
    srcs = ["sample_observers_test.py"],
    deps = [
        ":sample_observers",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:crypto",
        "//labm8/py:fs",
        "//labm8/py:test",
    ],
)

py_library(
    name = "samplers",
    srcs = ["samplers.py"],
    visibility = ["//visibility:public"],
    deps = [
        ":cache",
        ":errors",
        "//deeplearning/clgen/corpuses:atomizers",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:crypto",
        "//labm8/py:pbutil",
    ],
)

py_test(
    name = "samplers_test",
    srcs = ["samplers_test.py"],
    deps = [
        ":conftest",
        ":errors",
        ":samplers",
        "//labm8/py:app",
        "//labm8/py:test",
    ],
)

py_library(
    name = "samples_database",
    srcs = ["samples_database.py"],
    visibility = ["//visibility:public"],
    deps = [
        ":sample_observers",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:crypto",
        "//labm8/py:labdate",
        "//labm8/py:pbutil",
        "//labm8/py:sqlutil",
        "//third_party/py/sqlalchemy",
    ],
)

py_test(
    name = "samples_database_test",
    srcs = ["samples_database_test.py"],
    deps = [
        ":samples_database",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:test",
        "//third_party/py/pytest",
    ],
)

py_library(
    name = "telemetry",
    srcs = ["telemetry.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:jsonutil",
        "//labm8/py:labdate",
        "//labm8/py:pbutil",
    ],
)

py_test(
    name = "telemetry_test",
    srcs = ["telemetry_test.py"],
    deps = [
        ":telemetry",
        "//labm8/py:app",
        "//labm8/py:test",
    ],
)
