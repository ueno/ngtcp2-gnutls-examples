project('ngtcp2-gnutls-examples', 'c', 'cpp',
       default_options: ['cpp_std=c++17'])

cpp = meson.get_compiler('cpp')

nghttp3 = dependency('libnghttp3')
ngtcp2 = dependency('libngtcp2')
ngtcp2_crypto_gnutls = dependency('libngtcp2_crypto_gnutls')
gnutls = dependency('gnutls')

libev = cpp.find_library('ev')
if not cpp.has_function('ev_time', dependencies: libev)
  error('could not find libev')
endif

conf = configuration_data()

if cpp.has_header('arpa/inet.h')
  conf.set('HAVE_ARPA_INET_H', 1)
endif

if cpp.has_header('netinet/in.h')
  conf.set('HAVE_NETINET_IN_H', 1)
endif

configure_file(output: 'config.h', configuration: conf)

configinc = include_directories('.')

add_project_arguments(['-DHAVE_CONFIG_H=1'],
                      language: 'cpp')

libhttp_parser = static_library('http_parser',
				['http-parser/http_parser.c'])

libshared = static_library('shared', ['debug.cc',
				      'util.cc',
				      'keylog.cc',
				      'shared.cc'],
			   dependencies: [nghttp3, ngtcp2, gnutls])

executable('client', ['client.cc'],
	   link_with: [libshared, libhttp_parser],
	   include_directories: [configinc],
	   dependencies: [nghttp3, ngtcp2, ngtcp2_crypto_gnutls, gnutls, libev])

executable('server', ['server.cc', 'http.cc'],
	   link_with: [libshared, libhttp_parser],
	   include_directories: [configinc],
	   dependencies: [nghttp3, ngtcp2, ngtcp2_crypto_gnutls, gnutls, libev])
