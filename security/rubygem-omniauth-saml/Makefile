# Created by: Torsten Zuhlsdorff <ports@toco-domains.de>
# $FreeBSD$

PORTNAME=	omniauth-saml
PORTVERSION=	1.5.0
CATEGORIES=	security rubygems
MASTER_SITES=	RG

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	OmniAuth strategy for SAML

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE.md

RUN_DEPENDS=	rubygem-omniauth>=1.3:security/rubygem-omniauth \
		rubygem-ruby-saml>=1.1.1:security/rubygem-ruby-saml

NO_ARCH=	yes
USE_RUBY=	yes
USE_RUBYGEMS=	yes
RUBYGEM_AUTOPLIST=	yes

.include <bsd.port.mk>
