# Created by: Maxim Sobolev <sobomax@FreeBSD.org>
# $FreeBSD$

PORTNAME=	sippy_b2bua
PORTVERSION=	1.0.2
PORTREVISION=	3
CATEGORIES=	net python
MASTER_SITES=	http://www.b2bua.org/chrome/site/
DISTNAME=	sippy-${PORTVERSION}

MAINTAINER=	python@FreeBSD.org
COMMENT=	SIP Back-to-back user agent (B2BUA) server with Radius support

DEPRECATED=	Unmaintained, uses EOLed python27
EXPIRATION_DATE=	2020-01-27

BROKEN=		unfetchable

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}twisted>=0:devel/py-twisted@${PY_FLAVOR}

NO_ARCH=	yes
USE_PYTHON=	distutils
USES=		python:2.7
PYDISTUTILS_PKGNAME=	sippy
DOCSDIR=	${PREFIX}/share/doc/${PYDISTUTILS_PKGNAME}

DOCS=		COPYING README

OPTIONS_DEFINE=	DOCS

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${DOCS} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
