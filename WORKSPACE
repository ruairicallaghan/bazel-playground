
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

############## Go 

RULES_GO_VERSION = "0.33.0"
RULES_GO_SHA = "685052b498b6ddfe562ca7a97736741d87916fe536623afb7da2824c0211c369"

GAZELLE_VERSION = "0.25.0"
GAZELLE_SHA = "5982e5463f171da99e3bdaeff8c0f48283a7a5f396ec5282910b9e8a49c0dd7e"

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "685052b498b6ddfe562ca7a97736741d87916fe536623afb7da2824c0211c369",
    urls = [
      "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v%s/rules_go-v%s.zip" % (RULES_GO_VERSION, RULES_GO_VERSION),
      "https://github.com/bazelbuild/rules_go/releases/download/v%s/rules_go-v%s.zip" % (RULES_GO_VERSION, RULES_GO_VERSION),
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = GAZELLE_SHA,
    urls = [
      "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v%s/bazel-gazelle-v%s.tar.gz" % (GAZELLE_VERSION, GAZELLE_VERSION),
      "https://github.com/bazelbuild/bazel-gazelle/releases/download/v%s/bazel-gazelle-v%s.tar.gz" % (GAZELLE_VERSION, GAZELLE_VERSION),
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.18.3")

gazelle_dependencies()

############### Docker

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "b1e80761a8a8243d03ebca8845e9cc1ba6c82ce7c5179ce2b295cd36f7e394bf",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.25.0/rules_docker-v0.25.0.tar.gz"],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)

container_pull(
  name = "java_base",
  registry = "gcr.io",
  repository = "distroless/java",
  # 'tag' is also supported, but digest is encouraged for reproducibility.
  digest = "sha256:deadbeef",
)

load("@io_bazel_rules_docker//repositories:repositories.bzl", container_repositories = "repositories")

container_repositories()

load(
    "@io_bazel_rules_docker//java:image.bzl",
    _java_image_repos = "repositories",
)

_java_image_repos()

