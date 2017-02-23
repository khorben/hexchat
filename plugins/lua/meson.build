lua_dep = dependency('luajit')

shared_module('lua', 'lua.c',
  dependencies: [libgio_dep, hexchat_plugin_dep, lua_dep],
  install: true,
  install_dir: plugindir,
  name_prefix: '',
)