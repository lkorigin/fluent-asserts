project('fluent-asserts', 'd',
    meson_version: '>=0.42',
    license: 'MIT',
    version: '0.6.7'
)

project_soversion = '0'

#
# Dependencies
#
pkgc = import('pkgconfig')
ddmp_dep = dependency('ddmp', version: '>= 0.0.1', fallback: ['ddmp', 'ddmp_dep'])

#
# Sources
#
fluent_asserts_src = [
    'source/fluent/asserts.d',
    'core/fluentasserts/core/array.d',
    'core/fluentasserts/core/base.d',
    'core/fluentasserts/core/basetype.d',
    'core/fluentasserts/core/callable.d',
    'core/fluentasserts/core/objects.d',
    'core/fluentasserts/core/results.d',
    'core/fluentasserts/core/string.d'
]

core_src_dir = include_directories('core/')
src_dir = include_directories('source/')

#
# Targets
#
fluent_asserts_lib = library('fluent-asserts',
        [fluent_asserts_src],
        include_directories: [core_src_dir],
        dependencies: [ddmp_dep],
        install: true,
        version: meson.project_version(),
        soversion: project_soversion
)
pkgc.generate(name: 'fluent-asserts',
              libraries: fluent_asserts_lib,
              subdirs: 'd/fluentasserts',
              version: meson.project_version(),
              requires: 'ddmp',
              description: 'DLang fluent assertions done right.'
)

# to allow others to easily use this as a subproject
fluentasserts_dep = declare_dependency(
    link_with: [fluent_asserts_lib],
    include_directories: [core_src_dir, src_dir],
    dependencies: [ddmp_dep]
)

#
# Tests
#
fluent_asserts_test_exe = executable('fluentasserts-test',
    [fluent_asserts_src, 'test/emptymain.d'],
    include_directories: [core_src_dir, src_dir],
    dependencies: [ddmp_dep],
    d_unittest: true
)
test('fluentasserts-test',
    fluent_asserts_test_exe,
    workdir: meson.source_root()
)

#
# Install
#
install_subdir('core/fluentasserts/', install_dir: 'include/d/fluentasserts/')
install_subdir('source/fluent/', install_dir: 'include/d/fluentasserts/')
