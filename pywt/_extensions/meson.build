# Get math library (-lm) in portable way
cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required : false)

incdir_numpy = run_command(py3,
  ['-c', 'import numpy; print(numpy.get_include())'],
  check : true
).stdout().strip()

incdirs = include_directories(['c', incdir_numpy])

# This is a little annoying - we want to install _c99_config.py but
# not config.pxi. Also we are using the output in the cythonize custom_target
# to ensure config.pxi gets generated first. This may need a cleanup.
c99_config = custom_target('c99_config',
  build_by_default : true,
  install : true,
  install_dir : '.',
  output : ['_c99_config.py', 'config.pxi'],
  input : '_gen_c99_config.py',
  command : [py3, '@INPUT@', '@OUTPUT0@', '@OUTPUT1@'],
)

cythonize = custom_target('cythonize',
  build_by_default : true,
  output : ['_pywt.c', '_dwt.c', '_cwt.c', '_swt.c'],
  input : ['cythonize.py', '.', c99_config[0]],
  command : [py3, '@INPUT@', '@OUTPUT@'],
)


sources = [
  'c/common.c',
  'c/convolution.c',
  'c/cwt.c',
  'c/wavelets.c',
  'c/wt.c',
]
source_templates = [
  'c/convolution.template.c',
  'c/cwt.template.c',
  'c/wt.template.c',
]
headers = [
  'c/templating.h',
  'c/wavelets_coeffs.h',
  'c/common.h',
  'c/convolution.h',
  'c/wt.h',
  'c/wavelets.h',
  'c/cwt.h',
]
header_templates = [
  'c/convolution.template.h',
  'c/wavelets_coeffs.template.h',
  'c/cwt.template.h',
  'c/wt.template.h',
]

c_sources_all = [
  sources,
  source_templates,
  headers,
  header_templates,
]

# TODO: build libc_wt, then use it from extensions
libc_wt = library('c_wt',
  sources,
  c_args : '-DPY_EXTENSION',
  include_directories : incdirs,
  dependencies : [py3_dep, m_dep])

ext_pywt = py3.extension_module('_pywt',
  sources :[cythonize[0], sources],
  include_directories : incdirs,
  dependencies : [py3_dep, m_dep],
  link_with : libc_wt)

ext_dwt = py3.extension_module('_dwt',
  sources : [cythonize[1], sources],
  include_directories : incdirs,
  dependencies : [py3_dep, m_dep],
  link_with : libc_wt)

ext_cwt = py3.extension_module('_cwt',
  sources : [cythonize[2], sources],
  include_directories : incdirs,
  dependencies : [py3_dep, m_dep],
  link_with : libc_wt)

ext_swt = py3.extension_module('_swt',
  sources : [cythonize[3], sources],
  include_directories : incdirs,
  dependencies : [py3_dep, m_dep],
  link_with : libc_wt)
