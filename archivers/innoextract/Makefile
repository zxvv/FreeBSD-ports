# Created by: Nikolai Lifanov <lifanov@mail.lifanov.com>
# $FreeBSD$

PORTNAME=	innoextract
PORTVERSION=	1.6
CATEGORIES=	archivers
MASTER_SITES=	http://constexpr.org/innoextract/files/

MAINTAINER=	lifanov@mail.lifanov.com
COMMENT=	Program to extract Inno Setup files

LICENSE=	ZLIB
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libboost_iostreams.so:devel/boost-libs \
		libboost_filesystem.so:devel/boost-libs \
		libboost_system.so:devel/boost-libs \
		libboost_program_options.so:devel/boost-libs

USES=		cmake iconv
CMAKE_ARGS=	-DCMAKE_INSTALL_MANDIR=man

PLIST_FILES=	bin/innoextract \
		man/man1/innoextract.1.gz

.include <bsd.port.mk>
