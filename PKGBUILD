# Maintainer: Alexander Kuznecov <akuznecov@adyax.com>

_pkgname="nginx"
_user="http"
_group="http"
_doc_root="/usr/share/${_pkgname}/http"
_sysconf_path="etc"
_conf_path="${_sysconf_path}/${_pkgname}"
_tmp_path="/var/spool/${_pkgname}"
_pid_path="/var/run"
_lock_path="/var/lock"
_log_path="/var/log/${_pkgname}"

# 3d party modules versions:
_cachepurge_ver="2.0"
_slowfscache_ver="1.9"
_echo_ver="v0.41"
_headersmore_ver="v0.19"
_uploadprogress_ver="v0.8.4"
_upstreamfair_hash="a18b4099fbd458111983200e098b6f0c8efed4bc"
_fancyindex_ver="master"
_httpupload_ver="2.2.0"

pkgname=nginx-custom-dev
pkgver=1.3.10
pkgrel=1
pkgdesc="Development version of lightweight HTTP server and IMAP/POP3 proxy server with standard, additional and 3d party modules"
arch=('i686' 'x86_64')

depends=('pcre' 'zlib' 'openssl')
makedepends=(
	'libxslt'
	'gd'
)

url="http://nginx.org"
license=('custom')
conflicts=('nginx' 'nginx-unstable' 'nginx-svn' 'nginx-devel' 'nginx-custom') 
provides=('nginx')
backup=("${_conf_path#/}/conf/nginx.conf"
	"${_conf_path#/}/conf/koi-win"
	"${_conf_path#/}/conf/koi-utf"
	"${_conf_path#/}/conf/win-utf"
	"${_conf_path#/}/conf/mime.types"
	"${_conf_path#/}/conf/fastcgi.conf"
	"${_conf_path#/}/conf/fastcgi_params"
	"${_conf_path#/}/conf/scgi_params"
	"${_conf_path#/}/conf/uwsgi_params"
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
		"ngx_fancyindex-${_fancyindex_ver}::http://gitorious.org/ngx-fancyindex/ngx-fancyindex/archive-tarball/${_fancyindex_ver}"
		"https://github.com/vkholodkov/nginx-upload-module/tarball/${_httpupload_ver}"
		"http://nginx.org/patches/spdy/patch.spdy.txt"
		"nginx.sh"
		"nginx.conf"
		"nginx.logrotate"
		"nginx.service")

md5sums=('5ba0c4f713e803a14482a4137bde0fed'
         'b842d54d1a0e0c6a2c592e48d74357c1'
         'bc92b2d326e0ab937b4cf5ab489e71e3'
         '9a6acb984d81f5d7e04214d63ae94273'
         'e0f1c0cf4291387e8f5ac481cecd0ddd'
         '05b2c9dfacdce3201817a7a8b322c5b1'
         'ac5e7f485476af70e0ee1c52016cddaf'
         '8db9d2ef8b7ac63f9e23901dc3d36ab1'
         '8766b931f29602889e0454749580a781'
         '0cd3c15ebd87bdc8a90321f7eeb449b7'
         '0e8032d3ba26c3276e8c7c30588d375f'
         '1fe7a3ca0773ce13f9f92e239a99f8b9'
         '9dfca4c46969d3f620ed40b12c560637'
         'bc0b3c7096292162748ddc488df4995f')

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

	mv agentzh-headers-more-nginx-module-* ${_headersmore_dirname}
	mv agentzh-echo-nginx-module-* ${_echo_dirname}
	mv masterzen-nginx-upload-progress-module-* ${_uploadprogess_dirname}
	mv gnosek-nginx-upstream-fair-* ${_upstreamfair_dirname}
	mv ngx-fancyindex-ngx-fancyindex ${_fancyindex_dirname}
	mv vkholodkov-nginx-upload-module* ${_upload_dirname}

	cd $_src_dir

	patch -p0 < ../patch.spdy.txt

	./configure \
		--prefix="/${_conf_path}" \
		--sbin-path="/usr/sbin/${_pkgname}" \
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
		--with-http_gunzip_module \
		--add-module=../${_cachepurge_dirname} \
		--add-module=../${_echo_dirname} \
		--add-module=../${_headersmore_dirname} \
		--add-module=../${_slowfscache_dirname} \
		--add-module=../${_uploadprogess_dirname} \
		--add-module=../${_upstreamfair_dirname} \
		--add-module=../${_fancyindex_dirname}
		#--add-module=../${_upload_dirname}

	make
}

package() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	make DESTDIR="$pkgdir/" install

	sed -i -e "s/\<user\s\+\w\+;/user $_user;/g" $pkgdir/$_conf_path/conf/nginx.conf

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

