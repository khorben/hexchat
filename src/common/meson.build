common_sources = [
  'cfgfiles.c',
  'chanopt.c',
  'ctcp.c',
  'dcc.c',
  'hexchat.c',
  'history.c',
  'ignore.c',
  'inbound.c',
  'modes.c',
  'network.c',
  'notify.c',
  'outbound.c',
  'plugin.c',
  'plugin-identd.c',
  'plugin-timer.c',
  'proto-irc.c',
  'server.c',
  'servlist.c',
	'text.c',
  'tree.c',
  'url.c',
  'userlist.c',
  'util.c'
]

common_deps = [
  libgio_dep,
]

common_includes = [
  config_h_include,
  include_directories('.')
]

common_cflags = [
  '-DHAVE_CONFIG_H',
]

marshal = gnome.genmarshal('marshal',
  sources: 'marshalers.list',
  prefix: '_hexchat_marshal',
  internal: true
)

make_te = find_program('make-te.py')

textevents = custom_target('textevents',
  input: 'textevents.in',
  output: ['textevents.h', 'textenums.h'],
  command: [make_te, '@INPUT@', '@OUTPUT0@', '@OUTPUT1@']
)

# TODO:
#   LOOKUPD
#   SIGACTION
#   HAVE_GTK_MAC
#   WIN32
#   USING_FREEBSD

if get_option('with-ssl')
  common_sources += 'ssl.c'
  common_deps += libssl_dep
endif

if get_option('with-libproxy')
  common_deps += dependency('libproxy-1.0')
endif

if get_option('with-libcanberra')
  common_deps += dependency('libcanberra', version: '>= 0.22')
endif

if get_option('with-dbus')
  subdir('dbus')
  common_deps += hexchat_dbus_dep
  common_includes += include_directories('dbus')
endif

if get_option('with-plugin')
  common_deps += dependency('gmodule-2.0')
  common_cflags += '-DHEXCHATLIBDIR="@0@"'.format(join_paths(get_option('prefix'),
                                                  get_option('libdir'),
                                                  'hexchat/plugins'))
endif

hexchat_common = static_library('hexchatcommon',
  sources: [textevents] + marshal + common_sources,
  include_directories: config_h_include,
  dependencies: common_deps,
  c_args: common_cflags,
  pic: true
)

hexchat_common_dep = declare_dependency(
  link_with: hexchat_common,
  include_directories: common_includes,
  compile_args: common_cflags,
  dependencies: libgio_dep,
)
