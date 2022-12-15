project(
  'kaitai_struct_cpp_stl_runtime',
  'cpp',
  version : '0.10',
  default_options : ['default_library=static']
)

zlib = dependency('ZLIB')
iconv = dependency('iconv')
string_encoding_type = get_option('string_encoding_type')

deps = []
lib_args = []

if zlib.found()
  deps += zlib
  lib_args += '-DKS_ZLIB'
endif

if string_encoding_type == 'iconv'
  if iconv.found()
    deps += iconv
    lib_args += '-DKS_STR_ENCODING_ICONV'
  else
    error('iconv not found, but `string_encoding_type` is set to `iconv`')
  endif
elif string_encoding_type == 'none'
  lib_args += '-DKS_STR_ENCODING_NONE'
endif

kaitai_lib = shared_library(
  'kaitai_struct_cpp_stl_runtime',
  'kaitai/kaitaistream.cpp',
  include_directories : 'kaitai',
  cpp_args : lib_args,
  dependencies : deps,
)

kaitai_struct_cpp_stl_runtime_dep = declare_dependency(
  include_directories: 'kaitai',
  link_with : kaitai_lib,
)
