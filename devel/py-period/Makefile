# Created by: ijliao
# $FreeBSD$

PORTNAME=	period
PORTVERSION=	0.5
CATEGORIES=	devel python
MASTER_SITES=	http://www.biostat.wisc.edu/~annis/creations/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Basic time period checking library

USES=		python
NO_BUILD=	yes

OPTIONS_DEFINE=	DOCS

do-install:
	@${MKDIR} ${STAGEDIR}${PYTHON_SITELIBDIR}
	${INSTALL_SCRIPT} ${WRKSRC}/period.py ${STAGEDIR}${PYTHON_SITELIBDIR}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
.for ex in html txt
	${INSTALL_DATA} ${WRKSRC}/period.${ex} ${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.mk>
