# Created by: Sergey Matveychuk <sem@ciam.ru>
# $FreeBSD$

PORTNAME=	ace
PORTVERSION=	6.5.2
PORTREVISION=	2
CATEGORIES=	devel
MASTER_SITES=	ftp://download.dre.vanderbilt.edu/previous_versions/ \
		http://download.dre.vanderbilt.edu/previous_versions/
DISTNAME=	${PORTNAME:tu}-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Adaptive Communication Environment for C++

LICENSE=	ACE
LICENSE_NAME=	ACE
LICENSE_FILE=	${WRKSRC}/COPYING
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

BROKEN_powerpc=		Does not compile on ${ARCH}
BROKEN_sparc64=		Does not compile on ${ARCH}

USES=		compiler:c++11-lang gmake localbase:ldflags perl5 pkgconfig shebangfix tar:bzip2
USE_PERL5=	build
SHEBANG_FILES=	bin/*.pl MPC/*.pl
MAKE_ENV=	LD_LIBRARY_PATH="${WRKSRC}/lib" ACE_ROOT="${WRKSRC}" \
		CROSS-COMPILE=1
MAKEFILE=	GNUmakefile
USE_LDCONFIG=	yes

WRKSRC=		${WRKDIR}/ACE_wrappers

PLIST_SUB=	VERSION="${PORTVERSION}"

CONFLICTS=	ace+tao-5*

OPTIONS_DEFINE=		FLTK SSL TK TRIO X11
OPTIONS_DEFAULT=	SSL
OPTIONS_SUB=		yes

FLTK_DESC=		FLTK GUI toolkit
FLTK_LIB_DEPENDS=	libfltk.so:x11-toolkits/fltk
FLTK_MAKE_ENV=		fl=1
SSL_USES=		ssl
SSL_MAKE_ENV=		ssl=1
TK_USES=		tk
TK_MAKE_ENV=		tk=1
TRIO_DESC=		Trio portable string functions
TRIO_BUILD_DEPENDS=	trio>=0:devel/trio
TRIO_MAKE_ENV=		trio=1
X11_USES=		xorg
X11_USE=		XORG=xt
X11_MAKE_ENV=		xt=1

CPPFLAGS+=	-D_WANT_SEMUN

post-patch:
	@${REINPLACE_CMD} -e \
		's|/$$libdir/pkgconfig|/libdata/pkgconfig|g' \
		${WRKSRC}/bin/ace_install_pkgconfig.pl
	@${REINPLACE_CMD} -i "" -e \
		'/^C[CX]/s|\([[:space:]]\)=|\1?=| ; \
		 s|/usr/local|${LOCALBASE}| ; \
		 s|/usr/X11R6|${LOCALBASE}|' \
		${WRKSRC}/include/makeinclude/platform_freebsd.GNU

do-configure:
	@cd ${WRKSRC}/ace \
		&& ${ECHO_CMD} "#include <ace/config-${OPSYS:tl}.h>" >> config.h
	@cd ${WRKSRC}/include/makeinclude \
		&& ${ECHO_CMD} "include \$$(ACE_ROOT)/include/makeinclude/platform_${OPSYS:tl}.GNU" >> platform_macros.GNU \
		&& ${ECHO_CMD} "CC=	${CC}" >> platform_macros.GNU \
		&& ${ECHO_CMD} "CXX=	${CXX}" >> platform_macros.GNU \
		&& ${ECHO_CMD} "CPPFLAGS=	${CPPFLAGS}" >> platform_macros.GNU \
		&& ${ECHO_CMD} "LDFLAGS=	${LDFLAGS}" >> platform_macros.GNU \
		&& ${ECHO_CMD} "DCFLAGS=" >> platform_macros.GNU \
		&& ${ECHO_CMD} "OCFLAGS=	${CFLAGS}" >> platform_macros.GNU \
		&& ${ECHO_CMD} "INSTALL_PREFIX=	${PREFIX}" >> platform_macros.GNU \
		&& ${ECHO_CMD} "PLATFORM_TK_CPPFLAGS=	\$$(shell . ${TK_LIBDIR}/tkConfig.sh && ${ECHO_CMD} -n \$$\$$TK_INCLUDE_SPEC)" >> platform_macros.GNU \
		&& ${ECHO_CMD} "PLATFORM_TK_LIBS=	\$$(shell . ${TK_LIBDIR}/tkConfig.sh && ${ECHO_CMD} -n \$$\$$TK_LIB_FLAG)" >> platform_macros.GNU \
		&& ${ECHO_CMD} "PLATFORM_TCL_CPPFLAGS=	\$$(shell . ${TCL_LIBDIR}/tclConfig.sh && ${ECHO_CMD} -n \$$\$$TCL_INCLUDE_SPEC)" >> platform_macros.GNU \
		&& ${ECHO_CMD} "PLATFORM_TCL_LIBS=	\$$(shell . ${TCL_LIBDIR}/tclConfig.sh && ${ECHO_CMD} -n \$$\$$TCL_LIB_FLAG)" >> platform_macros.GNU

post-install:
	@for f in `${LS} -d \
		${STAGEDIR}${PREFIX}/lib/libACE*.so.${PORTVERSION} \
		${STAGEDIR}${PREFIX}/lib/libJAWS.so.${PORTVERSION} \
		${STAGEDIR}${PREFIX}/lib/libKokyu.so.${PORTVERSION} \
		| ${XARGS} ${BASENAME}`; do \
		n=`${ECHO_CMD} $${f}|${SED} -e 's/.so.${PORTVERSION}/.so/'`; \
		${LN} -sf $${n}.${PORTVERSION} ${STAGEDIR}${PREFIX}/lib/$${n}.6; \
		${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/$${n}.${PORTVERSION}; \
	done

.include <bsd.port.mk>
