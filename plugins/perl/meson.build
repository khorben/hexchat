perl_gen_header = find_program('generate_header')
perl = find_program('perl')
perl_headers = custom_target('perl-gen-headers',
  input: [
    'lib/HexChat.pm', 'lib/Xchat.pm', 'lib/HexChat/Embed.pm',
    'lib/HexChat/List/Network.pm', 'lib/HexChat/List/Network/Entry.pm',
    'lib/HexChat/List/Network/AutoJoin.pm', 'lib/IRC.pm'
  ],
  output: ['hexchat.pm.h', 'irc.pm.h'],
  command: [perl_gen_header]
)

ret = run_command([perl, '-MExtUtils::Embed', '-e', 'ccopts'])
if ret.returncode() != 0
  error('perl: Failed to get cflags')
endif
perl_cflags = ret.stdout().strip().split(' ')

ret = run_command([perl, '-MExtUtils::Embed', '-e', 'ldopts'])
if ret.returncode() != 0
  error('perl: Failed to get ldflags')
endif
perl_ldflags = ret.stdout().strip().split(' ')

shared_module('perl', ['perl.c', perl_headers],
  dependencies: [libgio_dep, hexchat_plugin_dep],
  c_args: perl_cflags,
  link_args: perl_ldflags,
  install: true,
  install_dir: plugindir,
  name_prefix: '',
)