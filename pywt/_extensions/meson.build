pyx_c = custom_target('_pywt',
  output : '_pywt.c',
  input : '_pywt.pyx',
  command : [cython, '@INPUT@', '-o', '@OUTPUT@'],
)

slib = py3.extension_module('_pywt',
  sources: pyx_c,
  dependencies : py3_dep)

# pydir = meson.current_build_dir()

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

