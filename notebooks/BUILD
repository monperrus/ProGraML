# Package containing Jupyter notebook servers.

# A Jupyter notebook server that includes a bunch of dependencies which I
# find useful. If you would like to include extra dependencies, create a new
# py_binary target with this target as the srcs, and add the dependencies:
#
#    py_binary(
#      name = "notebook",
#      srcs = ["//notebooks"],
#      deps = [
#          # Your dependencies here.
#      ],
#    )
#
# Use the run_notebooks.sh script to launch this target in the source tree:
# bash path/to/package/run_notebooks.sh.
py_binary(
    name = "notebooks",
    srcs = ["notebooks.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//labm8/py:app",
        "//labm8/py:bazelutil",
        "//labm8/py:jsonutil",
        "//labm8/py:labdate",
        "//labm8/py:labtypes",
        "//labm8/py:logutil",
        "//labm8/py:pbutil",
        "//labm8/py:pdutil",
        "//labm8/py:prof",
        "//labm8/py:sqlutil",
        "//labm8/py:viz",
        "//third_party/py/bokeh",
        "//third_party/py/fs",
        "//third_party/py/graph_nets",
        "//third_party/py/jupyter",
        "//third_party/py/keras",
        "//third_party/py/matplotlib",
        "//third_party/py/numpy",
        "//third_party/py/pandas",
        "//third_party/py/scikit_learn",
        "//third_party/py/scipy",
        "//third_party/py/seaborn",
        "//third_party/py/sonnet",
        "//third_party/py/tensorflow",
    ],
)
