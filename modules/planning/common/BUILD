load("//tools:cpplint.bzl", "cpplint")

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "indexed_list",
    hdrs = [
        "indexed_list.h",
    ],
    linkopts = [
        "-lboost_thread",
    ],
    deps = [
        "//modules/common/util:map_util",
    ],
)

cc_test(
    name = "indexed_list_test",
    size = "small",
    srcs = [
        "indexed_list_test.cc",
    ],
    deps = [
        ":indexed_list",
        "//modules/common/util",
        "@gtest//:main",
    ],
)

cc_library(
    name = "indexed_queue",
    hdrs = [
        "indexed_queue.h",
    ],
    deps = [
        "//modules/common/util:map_util",
    ],
)

cc_test(
    name = "indexed_queue_test",
    size = "small",
    srcs = [
        "indexed_queue_test.cc",
    ],
    deps = [
        ":indexed_queue",
        "//modules/common/util",
        "@gtest//:main",
    ],
)

cc_library(
    name = "obstacle",
    srcs = [
        "obstacle.cc",
    ],
    hdrs = [
        "obstacle.h",
    ],
    deps = [
        ":indexed_list",
        "//modules/common/math:box2d",
        "//modules/common/math:polygon2d",
        "//modules/common/util",
        "//modules/perception/proto:perception_proto",
        "//modules/planning/common:planning_gflags",
        "//modules/planning/common:planning_util",
        "//modules/planning/proto:planning_proto",
        "//modules/prediction/proto:prediction_proto",
    ],
)

filegroup(
    name = "common_testdata",
    srcs = glob([
        "testdata/**",
    ]),
)

cc_test(
    name = "obstacle_test",
    size = "small",
    srcs = [
        "obstacle_test.cc",
    ],
    data = [
        "//modules/planning/common:common_testdata",
    ],
    deps = [
        ":obstacle",
        "//modules/common/util",
        "//modules/perception/proto:perception_proto",
        "@gtest//:main",
    ],
)

cc_library(
    name = "path_obstacle",
    srcs = [
        "path_obstacle.cc",
    ],
    hdrs = [
        "path_obstacle.h",
    ],
    deps = [
        ":indexed_list",
        ":obstacle",
        "//modules/common/configs:vehicle_config_helper",
        "//modules/common/util:map_util",
        "//modules/planning/common/speed:st_boundary",
        "//modules/planning/proto:planning_proto",
        "//modules/planning/reference_line",
    ],
)

cc_test(
    name = "path_obstacle_test",
    size = "small",
    srcs = [
        "path_obstacle_test.cc",
    ],
    deps = [
        ":path_obstacle",
        "@gtest//:main",
    ],
)

cc_library(
    name = "planning_util",
    srcs = [
        "planning_util.cc",
    ],
    hdrs = [
        "planning_util.h",
    ],
    deps = [
        ":planning_gflags",
        "//modules/common/adapters:adapter_manager",
        "//modules/common/math",
        "//modules/common/proto:pnc_point_proto",
        "//modules/planning/math:hermite_spline",
        "//modules/planning/proto:planning_proto",
    ],
)

cc_library(
    name = "path_decision",
    srcs = [
        "path_decision.cc",
    ],
    hdrs = [
        "path_decision.h",
    ],
    deps = [
        ":obstacle",
        ":path_obstacle",
        "//modules/planning/reference_line",
    ],
)

cc_library(
    name = "planning_gflags",
    srcs = [
        "planning_gflags.cc",
    ],
    hdrs = [
        "planning_gflags.h",
    ],
    deps = [
        "//external:gflags",
    ],
)

cc_library(
    name = "reference_line_info",
    srcs = [
        "reference_line_info.cc",
    ],
    hdrs = [
        "reference_line_info.h",
    ],
    deps = [
        ":path_decision",
        "//modules/common:log",
        "//modules/common/proto:pnc_point_proto",
        "//modules/common/vehicle_state:vehicle_state_provider",
        "//modules/map/pnc_map",
        "//modules/map/proto:map_proto",
        "//modules/planning/common:planning_gflags",
        "//modules/planning/common/path:path_data",
        "//modules/planning/common/speed:speed_data",
        "//modules/planning/common/trajectory:discretized_trajectory",
        "//modules/planning/common/trajectory:publishable_trajectory",
        "//modules/planning/reference_line",
        "@eigen//:eigen",
    ],
)

cc_library(
    name = "frame",
    srcs = [
        "frame.cc",
    ],
    hdrs = [
        "frame.h",
    ],
    deps = [
        ":indexed_queue",
        ":obstacle",
        ":reference_line_info",
        "//modules/common:log",
        "//modules/common/adapters:adapter_manager",
        "//modules/common/configs:vehicle_config_helper",
        "//modules/common/vehicle_state:vehicle_state_provider",
        "//modules/map/hdmap:hdmap_util",
        "//modules/map/pnc_map",
        "//modules/planning/common/trajectory:discretized_trajectory",
        "//modules/planning/common/trajectory:publishable_trajectory",
        "//modules/planning/proto:planning_proto",
        "//modules/planning/reference_line:reference_line_provider",
    ],
)

cc_library(
    name = "speed_limit",
    srcs = [
        "speed_limit.cc",
    ],
    hdrs = [
        "speed_limit.h",
    ],
    deps = [
        "//modules/common/math",
        "//modules/planning/proto:planning_proto",
    ],
)

cc_test(
    name = "speed_limit_test",
    size = "small",
    srcs = [
        "speed_limit_test.cc",
    ],
    deps = [
        ":speed_limit",
        "@gtest//:main",
    ],
)

cc_library(
    name = "planning_common",
    deps = [
        ":frame",
        ":planning_gflags",
        ":speed_limit",
        "//modules/common:log",
        "//modules/localization/common:localization_common",
        "//modules/localization/proto:localization_proto",
        "@eigen//:eigen",
    ],
)

cpplint()
