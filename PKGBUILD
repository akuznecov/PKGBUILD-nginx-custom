# Maintainer: Alexander Kuznecov <alexander@kuznetcov.me>

_pkgname="nginx"
_user="http"
_group="http"
_doc_root="/usr/share/${_pkgname}/http"
_sysconf_path="etc"
_conf_path="${_sysconf_path}/${_pkgname}"
_tmp_path="/var/spool/${_pkgname}"
_pid_path="/run"
_lock_path="/var/lock"
_log_path="/var/log/${_pkgname}"

# 3d party modules versions:
_cachepurge_ver="2.1"
_slowfscache_ver="1.10"
_echo_ver="v0.45"
_headersmore_ver="v0.20"
_uploadprogress_ver="v0.9.0"
_upstreamfair_hash="a18b4099fbd458111983200e098b6f0c8efed4bc"
_fancyindex_ver="master"
_httpupload_ver="2.2.0"
_authpam_ver="1.2"
_pagespeed_ver="1.5.27.3"
_accesskey_ver="2.0.3"
_rtmp_ver="v1.0.0"

pkgname=nginx-custom
pkgver=1.4.1
pkgrel=1
pkgdesc="lightweight HTTP server and IMAP/POP3 proxy server with standard, additional and 3d party modules"
arch=('i686' 'x86_64')

depends=('pcre' 'zlib' 'openssl' 'pam' 'geoip' 'geoip-database')
makedepends=(
	'libxslt'
	'gd'
)

url="http://nginx.org"
license=('custom')
conflicts=('nginx' 'nginx-unstable' 'nginx-svn' 'nginx-devel' 'nginx-custom-dev') 
provides=('nginx')
backup=("${_conf_path}/nginx.conf"
	"${_conf_path}/koi-win"
	"${_conf_path}/koi-utf"
	"${_conf_path}/win-utf"
	"${_conf_path}/mime.types"
	"${_conf_path}/fastcgi.conf"
	"${_conf_path}/fastcgi_params"
	"${_conf_path}/scgi_params"
	"${_conf_path}/uwsgi_params"
	"etc/logrotate.d/nginx")
_user=http
_group=http

source=("http://nginx.org/download/nginx-$pkgver.tar.gz"
        "http://labs.frickle.com/files/ngx_cache_purge-${_cachepurge_ver}.tar.gz"
		"http://labs.frickle.com/files/ngx_slowfs_cache-${_slowfscache_ver}.tar.gz"
		"https://github.com/masterzen/nginx-upload-progress-module/tarball/${_uploadprogress_ver}"
		"https://github.com/agentzh/headers-more-nginx-module/tarball/${_headersmore_ver}"
		"https://github.com/agentzh/echo-nginx-module/tarball/${_echo_ver}"
		"https://github.com/gnosek/nginx-upstream-fair/tarball/${_upstreamfair_hash}"
		"ngx_fancyindex-${_fancyindex_ver}.tar.gz::http://gitorious.org/ngx-fancyindex/ngx-fancyindex/archive-tarball/${_fancyindex_ver}"
		"https://github.com/vkholodkov/nginx-upload-module/tarball/${_httpupload_ver}"
		"http://web.iti.upv.es/~sto/nginx/ngx_http_auth_pam_module-${_authpam_ver}.tar.gz"
		"https://github.com/pagespeed/ngx_pagespeed/archive/release-${_pagespeed_ver}-beta.zip"
		"https://dl.google.com/dl/page-speed/psol/${_pagespeed_ver}.tar.gz"
		"http://wiki.nginx.org/images/5/51/Nginx-accesskey-${_accesskey_ver}.tar.gz"
		"https://github.com/arut/nginx-rtmp-module/archive/${_rtmp_ver}.zip"
		"nginx.sh"
		"nginx.conf"
		"nginx.logrotate"
		"nginx.service")

md5sums=('fea7dfab995545ce27fe4c49dc21a972'
         'b403e963108f4e1700607cbe40916807'
         '68a1af12d5c1218fb2b3e05ed7ff6f0c'
         '9dd5dc90990dbaea68881a14d4b6d9f3'
         '85ddc984bcf83d113a06eee196579265'
         '851f882cf83732b2c70995227bdb07c6'
         'ac5e7f485476af70e0ee1c52016cddaf'
         '8db9d2ef8b7ac63f9e23901dc3d36ab1'
         '8766b931f29602889e0454749580a781'
         '3f6322663c6479a7b6b974bfa7417e5c'
         '17ab2fe221a20849f74d7c4954bbc0b3'
         'd8ff6fd166dcba74db46b597f5dc15ac'
         '9b5304346d5139b1841f5baa01ab0cbe'
         '103d12ffa1cf6988fccd2bece7da2b5d'
         'd56559ed5e8cc0b1c7adbe33f2300c4c'
         '845cab784b50f1666bbf89d7435ac7af'
         'ab1eb640c978536c1dad16674d6b3c3c'
         'ce9a06bcaf66ec4a3c4eb59b636e0dfd')

build() {
	local _src_dir="${srcdir}/${_pkgname}-${pkgver}"
	local _build_dir="${_src_dir}/objs"
	local _cachepurge_dirname="ngx_cache_purge-${_cachepurge_ver}"
	local _slowfscache_dirname="ngx_slowfs_cache-${_slowfscache_ver}"
	local _headersmore_dirname="ngx_headers_more-${_headersmore_ver}"
	local _echo_dirname="ngx_echo-${_echo_ver}"
	local _uploadprogess_dirname="ngx_upload_progress-${_uploadprogress_ver}"
	local _upstreamfair_dirname="ngx_upstream_fair"
	local _fancyindex_dirname="ngx_fancyindex"
	local _upload_dirname="ngx_http_upload-${_upload_ver}"
	local _authpam_dirname="ngx_authpam"
	local _pagespeed_dirname="ngx_pagespeed"
	local _accesskey_dirname="ngx_accesskey"
	local _rtmp_dirname="ngx_rtmp"

	mv agentzh-headers-more-nginx-module-* ${_headersmore_dirname}
	mv agentzh-echo-nginx-module-* ${_echo_dirname}
	mv masterzen-nginx-upload-progress-module-* ${_uploadprogess_dirname}
	mv gnosek-nginx-upstream-fair-* ${_upstreamfair_dirname}
	mv ngx-fancyindex* ${_fancyindex_dirname}
	mv vkholodkov-nginx-upload-module* ${_upload_dirname}
	mv ngx_http_auth_pam_module-${_authpam_ver} ${_authpam_dirname}
	mv ngx_pagespeed* ${_pagespeed_dirname}
	mv psol ${_pagespeed_dirname}/
	mv nginx-accesskey* ${_accesskey_dirname}
	mv nginx-rtmp-module* ${_rtmp_dirname}

	cd $_src_dir

	./configure \
		--prefix="/${_conf_path}" \
		--conf-path="/${_conf_path}/nginx.conf" \
		--sbin-path="/usr/bin/${_pkgname}" \
		--pid-path="${_pid_path}/${_pkgname}.pid" \
		--lock-path=${_pid_path}/${_pkgname}.lock \
		--http-client-body-temp-path=${_tmp_path}/client_body_temp \
		--http-proxy-temp-path=${_tmp_path}/proxy_temp \
		--http-fastcgi-temp-path=${_tmp_path}/fastcgi_temp \
		--http-uwsgi-temp-path=${_tmp_path}/uwsgi_temp \
		--http-scgi-temp-path=${_tmp_path}scgi_temp \
		--http-log-path=${_log_path}/access.log \
		--error-log-path=${_log_path}/error.log \
		--user=${_user} \
		--group=${_group} \
		--with-debug \
		--with-ipv6 \
		--with-imap \
		--with-imap_ssl_module \
		--with-http_ssl_module \
		--with-http_stub_status_module \
		--with-http_dav_module \
		--with-http_gzip_static_module \
		--with-http_realip_module \
		--with-http_addition_module \
		--with-http_xslt_module \
		--with-http_image_filter_module \
		--with-http_sub_module \
		--with-http_flv_module \
		--with-http_mp4_module \
		--with-http_random_index_module \
		--with-http_secure_link_module \
		--with-http_perl_module \
		--with-http_degradation_module \
		--with-http_geoip_module \
		--with-http_spdy_module \
		--with-http_gunzip_module \
		--add-module=../${_cachepurge_dirname} \
		--add-module=../${_echo_dirname} \
		--add-module=../${_headersmore_dirname} \
		--add-module=../${_slowfscache_dirname} \
		--add-module=../${_uploadprogess_dirname} \
		--add-module=../${_upstreamfair_dirname} \
		--add-module=../${_fancyindex_dirname} \
		--add-module=../${_authpam_dirname} \
		--add-module=../${_pagespeed_dirname} \
		--add-module=../${_accesskey_dirname} \
		--add-module=../${_rtmp_dirname}

		##--add-module=../${_upload_dirname} \

	make
}

package() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	make DESTDIR="$pkgdir/" install

	sed -i -e "s/\<user\s\+\w\+;/user $_user;/g" ${pkgdir}/$_conf_path/nginx.conf

	mkdir -p ${pkgdir}/$_conf_path/sites-enabled/
	mkdir -p ${pkgdir}/$_conf_path/sites-available/

	install -d "${pkgdir}/${_tmp_path}"
	install -d "${pkgdir}/${_doc_root}"

	mv "${pkgdir}/${_conf_path}/html/"* "${pkgdir}/${_doc_root}"
	rm -rf "${pkgdir}/${_conf_path}/html"

	install -D -m555 "${srcdir}/nginx.sh" "${pkgdir}/etc/rc.d/${_pkgname}"
	install -D -m644 "${srcdir}/nginx.logrotate" "${pkgdir}/etc/logrotate.d/${_pkgname}"
	install -D -m644 "${srcdir}/nginx.conf" "${pkgdir}/etc/conf.d/${_pkgname}"
	install -D -m644 "${srcdir}/nginx.service" "${pkgdir}/lib/systemd/system/nginx.service"
	install -D -m644 "LICENSE" "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
	install -D -m644 "man/nginx.8" "${pkgdir}/usr/share/man/man8/nginx.8"
}

