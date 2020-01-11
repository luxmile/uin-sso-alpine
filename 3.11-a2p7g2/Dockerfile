FROM ptipd/uin-devs-alpine:3.11-apache2-php7

MAINTAINER luxmile <luxmile@gmail.com>

COPY base/*.tar.bz2 /var/cache/apk/

RUN printf "Build of ptipd/uin-ssos-alpine:3.11-apache2-php7-llng2, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    sed -i 's#mod_rewrite.so#mod_rewrite.so\nLoadModule perl_module module/mod_perl.so#' /etc/apache2/httpd.conf && \
    #
    # install required perl modules:
    apk add apache-mod-fcgid perl-apache-session perl-cache-cache perl-config-inifiles perl-crypt-openssl-rsa \
        perl-crypt-x509 perl-crypt-openssl-random perl-crypt-rijndael perl-html-template perl-json perl-plack perl-uri perl-libwww && \
    #
    # prepare lemon-ldap handler dirs:
    mkdir -p /etc/lemonldap-ng \
        /usr/share/lemonldap-ng/bin \
        /usr/share/lemonldap-ng/ressources \
        /usr/share/lintian/overrides \
        /usr/share/perl5/Lemonldap/NG/Common/Apache/Session/Generate \
        /usr/share/perl5/Lemonldap/NG/Common/Apache/Session/Serialize \
        /usr/share/perl5/Lemonldap/NG/Common/Combination \
        /usr/share/perl5/Lemonldap/NG/Common/Conf/Backends \
        /usr/share/perl5/Lemonldap/NG/Common/Conf/SAML \
        /usr/share/perl5/Lemonldap/NG/Common/Logger \
        /usr/share/perl5/Lemonldap/NG/Common/Notifications \
        /usr/share/perl5/Lemonldap/NG/Common/PSGI/Cli \
        /usr/share/perl5/Lemonldap/NG/Common/Session \
        /usr/share/perl5/auto/Lemonldap/NG/Common/Apache/Session \
        /usr/share/perl5/auto/Lemonldap/NG/Common/Regexp \
        /var/lib/lemonldap-ng/conf \
        /var/lib/lemonldap-ng/psessions/lock \
        /var/lib/lemonldap-ng/sessions/lock && \
    cd / && \
    tar jxf /var/cache/apk/lemonldap-ng-handler.tar.bz2 && \
    tar jxf /var/cache/apk/apache2-mod_perl.tar.bz2 && \
    #
    # cleanup:
    rm -rf /var/cache/apk/*
