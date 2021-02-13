# pydir = meson.current_build_dir()
inc = include_directories('c')

c99_config =  custom_target('c99_config',
  output : ['_c99_config.py', 'config.pxi'],
  input : '_gen_c99_config.py',
  command : [py3, '@INPUT@', '@OUTPUT0@', '@OUTPUT1@'],
)

cythonize =  custom_target('cythonize',
  output : ['_pywt.c', '_dwt.c', '_cwt.c', '_swt.c'],
  input : c99_config,
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
  c99_config[1],
]

#_pywt_c = custom_target('_pywt',
#  output : '_pywt.c',
#  input : '_pywt.pyx',
#  command : [cython, '@INPUT@', '-o', '@OUTPUT@'],
#)

ext_pywt = py3.extension_module('_pywt',
  sources : cythonize[0],
#  include_directories : inc,
  dependencies : py3_dep)

#_dwt_c = custom_target('_dwt',
#  output : '_dwt.c',
#  input : '_dwt.pyx',
#  command : [cython, '@INPUT@', '-o', '@OUTPUT@'],
#)

ext_dwt = py3.extension_module('_dwt',
  sources : cythonize[1],
  dependencies : py3_dep)

#_cwt_c = custom_target('_cwt',
#  output : '_cwt.c',
#  input : '_cwt.pyx',
#  command : [cython, '@INPUT@', '-o', '@OUTPUT@'],
#)

ext_cwt = py3.extension_module('_cwt',
  sources : cythonize[2],
  dependencies : py3_dep)

#_swt_c = custom_target('_swt',
#  output : '_swt.c',
#  input : '_swt.pyx',
#  command : [cython, '@INPUT@', '-o', '@OUTPUT@'],
#)

ext_swt = py3.extension_module('_swt',
  sources : cythonize[3],
  dependencies : py3_dep)
