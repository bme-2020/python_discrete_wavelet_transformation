# pydir = meson.current_build_dir()
incdir_numpy = run_command(py3,
  ['-c', 'import numpy; print(numpy.get_include())'],
  check : true
).stdout().strip()

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


ext_pywt = py3.extension_module('_pywt',
  sources :[cythonize[0]],
  include_directories : incdir_numpy,
  dependencies : py3_dep)

ext_dwt = py3.extension_module('_dwt',
  sources : cythonize[1],
  include_directories : incdir_numpy,
  dependencies : py3_dep)

ext_cwt = py3.extension_module('_cwt',
  sources : cythonize[2],
  include_directories : incdir_numpy,
  dependencies : py3_dep)

ext_swt = py3.extension_module('_swt',
  sources : cythonize[3],
  include_directories : incdir_numpy,
  dependencies : py3_dep)
