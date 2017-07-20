macos_preprocessor_flags = [
  '-Wno-expansion-to-defined',
  '-DHAVE_PTHREAD=1',
]

linux_preprocessor_flags = [
  '-Wno-expansion-to-defined',
  '-DHAVE_PTHREAD=1',
]

linux_linker_flags = [
  '-lpthread',
]

cxx_library(
  name = 'protobuf',
  header_namespace = 'google',
  exported_headers = subdir_glob([
    ('src/google', 'protobuf/**/*.h'),
  ], excludes = glob([
    'src/google/protobuf/testing/*.h',
    'src/google/protobuf/**/*_test*.h',
    'src/google/protobuf/**/*test_*.h',
    'src/google/protobuf/**/*unittest*.h',
    'src/google/protobuf/**/*mock*.h',
  ])),
  srcs = glob([
    'src/google/protobuf/**/*.cc',
  ], excludes = glob([
    'src/google/protobuf/compiler/main.cc',
    'src/google/protobuf/compiler/js/embed.cc',
    'src/google/protobuf/compiler/js/js_generator.cc',
    'src/google/protobuf/testing/**/*.cc',
    'src/google/protobuf/**/*_test*.cc',
    'src/google/protobuf/**/*test_*.cc',
    'src/google/protobuf/**/*unittest*.cc',
    'src/google/protobuf/**/*mock*.cc',
  ])),
  platform_preprocessor_flags  = [
    ('^macos.*', macos_preprocessor_flags),
    ('^linux.*', linux_preprocessor_flags),
    ('default', linux_preprocessor_flags),
  ],
  platform_linker_flags = [
    ('^linux.*', linux_linker_flags),
  ],
  visibility = [
    'PUBLIC',
  ],
)

cxx_binary(
  name = 'protoc',
  srcs = [
    'src/google/protobuf/compiler/main.cc',
  ],
  preprocessor_flags = [
    '-DOPENSOURCE_PROTOBUF_CPP_BOOTSTRAP=1',
  ],
  platform_preprocessor_flags = [
    ('^macos.*', [ '-Wno-expansion-to-defined' ]),
    ('^linux.*', [ '-Wno-expansion-to-defined' ]),
    ('default', [ '-Wno-expansion-to-defined' ]),
  ],
  deps = [
    ':protobuf',
  ],
  visibility = [
    'PUBLIC',
  ],
)
