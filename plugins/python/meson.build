python_dep = dependency('python3', version: '>= 3.3')

shared_module('python', 'python.c',
  dependencies: [libgio_dep, hexchat_plugin_dep, python_dep],
  install: true,
  install_dir: plugindir,
  name_prefix: '',
)