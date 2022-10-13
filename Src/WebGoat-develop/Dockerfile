FROM ifixit:latest

RUN echo '<? return require_once "Conf/deployments/localdev.php";' > /etc/ifixit-deployment
RUN ln -sf /home/local/Code/Conf/roles/localdev/php.ini /etc/php.ini
RUN ln -snf /home/local/Code/Conf/roles/localdev /etc/ifixit-config

RUN dnf -y install perl-Digest-SHA

ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    pecl channel-update pecl.php.net && \
    pecl install xdebug-3.0.4 && \
    echo "zend_extension=xdebug.so" > /etc/php.d/xdebug.ini \
;fi

ARG INSTALL_MOD_SSL=false
RUN if [ ${INSTALL_MOD_SSL} = true ]; then \
    dnf -y install mod_ssl \
;fi

ARG NAVE_INSTALL_VERSION=false
RUN if [ ${NAVE_INSTALL_VERSION} != false ]; then \
    npx nave install ${NAVE_INSTALL_VERSION} \
;fi

RUN useradd -G apache local && chmod 755 /home/local
