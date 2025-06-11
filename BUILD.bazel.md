
latex_document(
    name = "repro",
    srcs = [
        "@bazel_latex//packages:amsmath",
    ],
    main = "repro.tex",
)