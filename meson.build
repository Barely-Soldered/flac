project(
  'flac',
  'c',
  version: '1.5.0',
  license: 'BSD-3-Clause',
  meson_version: '>= 1.0.0',
  default_options: [
    'c_std=c99',
    'warning_level=1',
    'default_library=static',
  ],
)

ogg_dep = dependency('ogg')

flac_sources = files(
  'src/bitmath.c',
  'src/bitreader.c',
  'src/bitwriter.c',
  'src/cpu.c',
  'src/crc.c',
  'src/fixed.c',
  'src/float.c',
  'src/format.c',
  'src/lpc.c',
  'src/md5.c',
  'src/memory.c',
  'src/metadata_iterators.c',
  'src/metadata_object.c',
  'src/ogg_decoder_aspect.c',
  'src/ogg_encoder_aspect.c',
  'src/ogg_helper.c',
  'src/ogg_mapping.c',
  'src/stream_decoder.c',
  'src/stream_encoder.c',
  'src/stream_encoder_framing.c',
  'src/window.c',
)

if host_machine.system() == 'windows'
  flac_sources += files('src/share/win_utf8_io.c')
endif

flac_c_args = [
  '-DHAVE_CONFIG_H',
  '-DFLAC__NO_DLL',
]

flac_internal_inc = include_directories('src', 'include')
flac_public_inc = include_directories('include', is_system: true)

flac_lib = static_library(
  'FLAC',
  flac_sources,
  c_args: flac_c_args,
  include_directories: flac_internal_inc,
  dependencies: ogg_dep,
)

flac_dep = declare_dependency(
  compile_args: ['-DFLAC__NO_DLL'],
  link_with: flac_lib,
  include_directories: flac_public_inc,
  dependencies: ogg_dep,
)

meson.override_dependency('flac', flac_dep)
