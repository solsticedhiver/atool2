project('atool2', version: '0.39.0')

conf_data = configuration_data()
conf_data.set('package_version', meson.project_version())
conf_data.set('package_name', 'atool')
conf_data.set('package_tarname', 'atool')
conf_data.set('package_string', conf_data.get('package_name')+ ' '+ conf_data.get('package_version'))
conf_data.set('package_bugreport', 'htpps://github.com/solsticedhiver/atool2/issues')
conf_data.set('package_url', 'htpps://github.com/solsticedhiver/atool2')
conf_data.set('sysconfdir', get_option('sysconfdir'))

configure_file(input : 'atool.in',
    output : 'atool',
    configuration : conf_data,
    install_dir: get_option('bindir'),
    install_mode: 'rwxr-xr-x')
configure_file(input : 'atool.spec.in',
    output : 'atool.spec',
    configuration : conf_data)
configure_file(input : 'atool.1.in',
    output : 'atool.1',
    configuration : conf_data,
    install_dir: get_option('mandir')+'/man1')

foreach link: ['aunpack', 'arepack', 'apack', 'acat', 'als', 'adiff']
    install_symlink(link, install_dir:get_option('bindir'), pointing_to:'atool')
    install_symlink(link, install_dir:get_option('mandir')+'/man1', pointing_to:'atool.1')
endforeach

dpbp = find_program('dpkg-buildpackage', required: false)
if dpbp.found()
    debian_pkg = custom_target('debian',
        output: conf_data.get('package_name')+'-'+conf_data.get('package_version')+'.deb',
        command: [dpbp, '-rfakeroot', '-us', '-uc', '-sd', '-b'])
endif

rpmbuild = find_program('rpmbuild', required: false)
if rpmbuild.found()
    rpm_pkg = custom_target('rpm',
        input: 'atool.spec',
        output: conf_data.get('package_name')+'-'+conf_data.get('package_version')+'.rpm',
        command: [rpmbuild, '-ba', '--clean', '@INPUT@'])
endif
