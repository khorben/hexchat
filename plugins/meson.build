plugindir = join_paths(get_option('libdir'), 'hexchat/plugins')

if target_machine.system() == 'windows'
  if get_option('with-exec') and
    subdir('exec')
  endif

  if get_option('with-mpcinfo')
    subdir('mpcinfo')
  endif

  if get_option('with-upd')
    subdir('upd')
  endif

  if get_option('with-winamp')
    subdir('winamp')
  endif
endif

if get_option('with-checksum')
  subdir('checksum')
endif

if get_option('with-fishlim')
  subdir('fishlim')
endif

if get_option('with-lua')
  subdir('lua')
endif

if get_option('with-perl')
  subdir('perl')
endif

if get_option('with-python')
  subdir('python')
endif

if get_option('with-sysinfo')
  subdir('sysinfo')
endif
