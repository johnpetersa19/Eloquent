desktop_file = i18n.merge_file(
  input: 're.sonny.Eloquent.desktop',
  output: 're.sonny.Eloquent.desktop',
  type: 'desktop',
  po_dir: '../po',
  install: true,
  install_dir: join_paths(get_option('datadir'), 'applications')
)

desktop_utils = find_program('desktop-file-validate', required: false)
if desktop_utils.found()
  test('Validate desktop file', desktop_utils,
    args: [desktop_file]
  )
endif

appstream_file = i18n.merge_file(
  input: 're.sonny.Eloquent.metainfo.xml',
  output: 're.sonny.Eloquent.metainfo.xml',
  po_dir: '../po',
  install: true,
  install_dir: join_paths(get_option('datadir'), 'metainfo')
)

service_conf = configuration_data()
service_conf.set('bindir', bindir)
configure_file(
  input: 're.sonny.Eloquent.service',
  output: 're.sonny.Eloquent.service',
  configuration: service_conf,
  install_dir: join_paths(get_option('datadir'), 'dbus-1/services')
)

appstreamcli = find_program('appstreamcli', required: true)
test(
  'Validate appstream file',
  appstreamcli,
  args: ['validate', '--no-net', '--explain', appstream_file],
)

install_data('re.sonny.Eloquent.gschema.xml',
  install_dir: join_paths(get_option('datadir'), 'glib-2.0/schemas')
)

compile_schemas = find_program('glib-compile-schemas', required: false)
if compile_schemas.found()
  test('Validate schema file', compile_schemas,
    args: ['--strict', '--dry-run', meson.current_source_dir()]
  )
endif

install_data('icons/re.sonny.Eloquent.svg', install_dir: join_paths(get_option('datadir'), 'icons/hicolor/scalable/apps'))
install_data('icons/re.sonny.Eloquent-symbolic.svg', install_dir: join_paths(get_option('datadir'), 'icons/hicolor/symbolic/apps'))

install_data('server.properties', install_dir: join_paths(get_option('datadir')))
