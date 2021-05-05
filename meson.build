project('elas', 'cpp', default_options : ['cpp_std=c++17', 'warning_level=0', 'optimization=2'])

cpp = meson.get_compiler('cpp')
elas_lib_cpp_args = cpp.get_supported_arguments(['-msse3'])

elas_dep_comp_args = []
if get_option('elas_profiler')
  elas_dep_comp_args += '-DPROFILE=true'
endif

opencvdep = dependency('opencv4')

inc = include_directories('include')

srcElas = ['src/elas.cpp', 'src/descriptor.cpp', 'src/filter.cpp', 'src/matrix.cpp', 'src/triangle.cpp']

# Library generation
headersLibrary = ['include/elas.h']

install_headers( headersLibrary )

elas_lib = library(
  'elas',
  srcElas,
  include_directories : inc,
  dependencies : [ opencvdep ],
  cpp_args : [elas_dep_comp_args, elas_lib_cpp_args],
  override_options : 'warning_level=0',
  install : true
  )

elas_dep = declare_dependency(
  include_directories : inc,
  dependencies : [opencvdep],
  link_with : elas_lib,
  compile_args : elas_dep_comp_args
  )

executable('example',
  sources : ['src/main.cpp'],
  dependencies : [elas_dep]
  )
