# Created by: mdodd
# $FreeBSD$

PORTNAME=	scorched3d
PORTVERSION=	0.${SCORCH_VERSION}${SCORCH_REVISION}
PORTREVISION=	9
CATEGORIES=	games
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/Version%20${SCORCH_VERSION}
DISTNAME=	Scorched3D-${SCORCH_VERSION}-src

MAINTAINER=	ports@FreeBSD.org
COMMENT=	3D version of the classic DOS game Scorched Earth

LICENSE=	GPLv2

LIB_DEPENDS=	libvorbis.so:audio/libvorbis \
		libpng.so:graphics/png \
		libfftw3.so:math/fftw3 \
		libfftw3f.so:math/fftw3-float \
		libexpat.so:textproc/expat2

OPTIONS_DEFINE=	MYSQL

WRKSRC=		${WRKDIR}/scorched

USE_GL=		glew glu
USE_SDL=	mixer net sdl
USE_WX=		2.8
WX_CONF_ARGS=	absolute
WX_UNICODE=	yes
USES=		autoreconf dos2unix gmake iconv jpeg openal:al,alut perl5 pkgconfig
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--datadir=${DATADIR}

DOS2UNIX_FILES=	src/client/GLEXT/GLFont2dFreeType.h \
		src/launcher/wxdialogs/TrueTypeFont.h

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

SCORCH_VERSION=		43.3d
SCORCH_REVISION=	# none

MYSQL_USE=	MYSQL=yes
MYSQL_CONFIGURE_ON=	--with-mysql

PLIST_FILES=	bin/scorched3d \
		bin/scorched3dc \
		bin/scorched3ds
PORTDATA=	*

post-extract:
	@${RM} -f ${WRKSRC}/src/client/GLEXT/[a-z]*

post-patch:
	@${REINPLACE_CMD} -e \
		'/^CPPFLAGS=/s|^|#|g ; \
		 /^LDFLAGS=/s|^|#|g ; \
		 /if test/s|==|=|' ${WRKSRC}/configure.ac
	@${REINPLACE_CMD} -e \
		'/GL_LIBS/s|"-lGL -lGLU"|"-lGL -lGLU -lGLEW"| ; \
		 /if test/s|==|=|' ${WRKSRC}/*.m4
	@${REINPLACE_CMD} -e \
		's|std::exit|exit|' ${WRKSRC}/src/common/common/main.h
	@${REINPLACE_CMD} -e \
		's|"glew.h"|<GL/glew.h>|' ${WRKSRC}/src/client/GLEXT/GLState.h
	@${REINPLACE_CMD} -e \
		'/GLEXT\\glew.c/d ; \
		 /GLEXT\\glew.h/d ; \
		 /GLEXT\\glxew.h/d ; \
		 /GLEXT\\wglew.h/d' ${WRKSRC}/src/client/scorchedc/scorchedc.vcxproj

pre-configure:
	@cd ${WRKSRC}/scripts && ${PERL} createAMMakefile.pl

.include <bsd.port.mk>
