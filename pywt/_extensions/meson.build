pyx_c = custom_target('_pywt',
  output : '_pywt.c',
  input : '_pywt.pyx',
  command : [cython, '@INPUT@', '-o', '@OUTPUT@'],
)

slib = py3.extension_module('_pywt',
  sources: pyx_c,
  dependencies : py3_dep)

# pydir = meson.current_build_dir()
