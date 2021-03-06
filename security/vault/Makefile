# $FreeBSD$

PORTNAME=	vault
PORTVERSION=	0.3.0
DISTVERSIONPREFIX=	v
CATEGORIES=	security

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Tool for securely accessing secrets

LICENSE=	MPL

BUILD_DEPENDS=	${LOCALBASE}/bin/go:lang/go

USE_GITHUB=	yes
GH_ACCOUNT=	hashicorp

STRIP=		# stripping can break go binaries

USE_RC_SUBR=	vault

USERS=		vault
GROUPS=		vault

PLIST_FILES=	bin/${PORTNAME}

post-extract:
	@${MV} ${WRKSRC}/Godeps/_workspace/src ${WRKSRC}
	@${MKDIR} ${WRKSRC}/src/github.com/${GH_ACCOUNT}/${PORTNAME}
	@cd ${WRKSRC} ; \
	${MV} .gitignore .travis.yml CHANGELOG.md LICENSE Makefile README.md \
	api audit builtin cli command helper http logical main.go main_test.go \
	make.bat physical scripts shamir terraform test vault website \
	src/github.com/${GH_ACCOUNT}/${PORTNAME}

do-build:
	@cd ${WRKSRC}/src/github.com/${GH_ACCOUNT}/${PORTNAME}; \
		${SETENV} ${BUILD_ENV} GOPATH=${WRKSRC} go build -o bin/${PORTNAME}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/src/github.com/${GH_ACCOUNT}/${PORTNAME}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}

.include <bsd.port.mk>
