# Created by: Hung-Yi Chen <gaod@hychen.org>
# $FreeBSD$

PORTNAME=	watchlist
PORTVERSION=	1.0.${SVN_REV}
PORTREVISION=	4
CATEGORIES=	www devel python
MASTER_SITES=	http://distfiles.cse.tw/ \
		http://trac-hacks.org/changeset/${SVN_REV}/watchlistplugin?old_path=/&format=zip&filename=/
PKGNAMEPREFIX=	trac-
DISTNAME=	${PORTNAME}plugin-r${SVN_REV}

MAINTAINER=	gaod@hychen.org
COMMENT=	Watchlist feature for wikis and tickets of Trac

BROKEN=		unfetchable
DEPRECATED=	Broken, uses EOLed python27
EXPIRATION_DATE=	2020-02-19

LICENSE=	GPLv3+

RUN_DEPENDS=	tracd:www/trac

SVN_REV=	11526

WRKSRC=		${WRKDIR}/${PORTNAME}plugin/0.12
USES=		python:2.7 zip
USE_PYTHON=	distutils autoplist
NO_ARCH=	yes

FETCH_BEFORE_ARGS=	-o ${DISTFILES}

.include <bsd.port.mk>
