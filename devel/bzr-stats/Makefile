# Created by: Carlo Strub
# $FreeBSD$

PORTNAME=	bzr-stats
PORTVERSION=	0.1.0
PORTREVISION=	1
CATEGORIES=	devel
MASTER_SITES=	http://launchpadlibrarian.net/65203347/ \
		http://www.c-s.li/ports/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Simple statistics plugin for bzr

BUILD_DEPENDS=	bzr:devel/bzr
RUN_DEPENDS=	bzr:devel/bzr

LICENSE=	GPLv2

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}

USES=		python
USE_PYTHON=	distutils autoplist

.include <bsd.port.mk>
