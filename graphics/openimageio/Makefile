# Created by: Shane Ambler <FreeBSD@Shaneware.biz>
# $FreeBSD$

PORTNAME=	openimageio
PORTVERSION=	1.6.10
DISTVERSIONPREFIX=	Release-
PORTREVISION?=	1
CATEGORIES?=	graphics multimedia

MAINTAINER?=	FreeBSD@Shaneware.biz
COMMENT?=	OpenImageIO graphics library

LICENSE=	BSD3CLAUSE

USE_GITHUB=	yes
GH_ACCOUNT=	OpenImageIO
GH_PROJECT=	oiio

# fbm also installs bin/idiff
CONFLICTS=	fbm-[0-9]*

USES=		cmake:outsource compiler:c11
CMAKE_ARGS=	-DBUILDSTATIC:BOOL=OFF \
		-DLINKSTATIC:BOOL=OFF \
		-DNOTHREADS:BOOL=OFF \
		-DSTOP_ON_WARNING:BOOL=OFF \
		-DOIIO_BUILD_CPP11:BOOL=OFF \
		-DOIIO_BUILD_CPP14:BOOL=OFF \
		-DUSE_OPENSSL:BOOL=OFF

OPTIONS_DEFINE=		DOCS FFMPEG FREETYPE GIF IMAGEVIEWER OCIO OPENCV \
			OPENJPEG RAW TEST
OPTIONS_DEFAULT=	FREETYPE GIF OCIO OPENJPEG
OPTIONS_SUB=		yes

FFMPEG_DESC=		Use FFmpeg to support extra file types
IMAGEVIEWER_DESC=	Build image viewer (requires Qt)
OCIO_DESC=		Color management support

DOCS_CMAKE_ON=		-DINSTALL_DOCS:BOOL=ON
DOCS_CMAKE_OFF=		-DINSTALL_DOCS:BOOL=OFF

FFMPEG_CMAKE_ON=	-DUSE_FFMPEG:BOOL=ON
FFMPEG_CMAKE_OFF=	-DUSE_FFMPEG:BOOL=OFF
FFMPEG_LIB_DEPENDS=	libavutil.so:multimedia/ffmpeg

FREETYPE_CMAKE_ON=	-DUSE_FREETYPE:BOOL=ON
FREETYPE_CMAKE_OFF=	-DUSE_FREETYPE:BOOL=OFF
FREETYPE_LIB_DEPENDS=	libfreetype.so:print/freetype2

GIF_CMAKE_ON=		-DUSE_GIF:BOOL=ON
GIF_CMAKE_OFF=		-DUSE_GIF:BOOL=OFF
GIF_LIB_DEPENDS=	libgif.so:graphics/giflib

IMAGEVIEWER_CMAKE_ON=	-DUSE_QT:BOOL=ON -DUSE_OPENGL:BOOL=ON
IMAGEVIEWER_CMAKE_OFF=	-DUSE_OPENGL:BOOL=OFF -DUSE_QT:BOOL=OFF
IMAGEVIEWER_USE=	GL=glew QT4=corelib,gui,opengl,qmake_build,moc_build,rcc_build,uic_build

OCIO_CMAKE_ON=		-DUSE_OCIO:BOOL=ON
OCIO_CMAKE_OFF=		-DUSE_OCIO:BOOL=OFF
OCIO_LIB_DEPENDS=	libOpenColorIO.so:graphics/opencolorio

OPENCV_CMAKE_ON=	-DUSE_OPENCV:BOOL=ON
OPENCV_CMAKE_OFF=	-DUSE_OPENCV:BOOL=OFF
OPENCV_LIB_DEPENDS=	libopencv_highgui.so:graphics/opencv

OPENJPEG_CMAKE_ON=	-DUSE_OPENJPEG:BOOL=ON
OPENJPEG_CMAKE_OFF=	-DUSE_OPENJPEG:BOOL=OFF
OPENJPEG_LIB_DEPENDS=	libopenjpeg.so:graphics/openjpeg15

RAW_CMAKE_ON=		-DUSE_LIBRAW:BOOL=ON
RAW_CMAKE_OFF=		-DUSE_LIBRAW:BOOL=OFF
RAW_LIB_DEPENDS=	libraw_r.so:graphics/libraw

TEST_CMAKE_ON=		-DOIIO_BUILD_TESTS:BOOL=ON
TEST_CMAKE_OFF=		-DOIIO_BUILD_TESTS:BOOL=OFF

PLIST_SUB+=		LIBVERS=${PORTVERSION}

.include <bsd.port.options.mk>

.if ${ARCH} == powerpc
USE_GCC=	yes
.endif

.if ${SLAVE_PORT} == no
LIB_DEPENDS+=	libIlmImf.so:graphics/OpenEXR \
		libboost_thread.so:devel/boost-libs \
		libhdf5.so:science/hdf5 \
		libwebp.so:graphics/webp
USE_LDCONFIG=	yes
CMAKE_ARGS+=	-DUSE_PYTHON:BOOL=OFF -DUSE_PYTHON3:BOOL=OFF \
		-DOIIO_BUILD_TOOLS:BOOL=ON
.else
LIB_DEPENDS=	libOpenImageIO.so:graphics/openimageio \
		libboost_python.so:devel/boost-python-libs
PLIST=		${PKGDIR}/pkg-plist-pybind
#while oiio supports py3, ports doesn't have py3 support for boost-python yet
USES+=		python:2
CMAKE_ARGS+=	-DUSE_PYTHON:BOOL=ON -DUSE_PYTHON3:BOOL=OFF \
		-DOIIO_BUILD_TOOLS:BOOL=OFF -DUSE_FFMPEG:BOOL=OFF
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|share/doc/OpenImageIO|${DOCSDIR}|g' \
		${WRKSRC}/CMakeLists.txt

post-install:
.if ${SLAVE_PORT} == no
	${LN} -sf libOpenImageIO.so.1.6 \
		${STAGEDIR}${PREFIX}/lib/libOpenImageIO.so.1
	${LN} -sf libOpenImageIO_Util.so.1.6 \
		${STAGEDIR}${PREFIX}/lib/libOpenImageIO_Util.so.1
.endif

do-test-TEST-on:
	@cd ${BUILD_WRKSRC} && ${MAKE_CMD} ARGS=-V test

.include <bsd.port.mk>
