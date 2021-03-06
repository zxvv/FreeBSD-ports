# Created by: gahr
# $FreeBSD$

PORTNAME=	mysql-connector-c++
PORTVERSION=	1.1.7
PORTREVISION=	1
CATEGORIES=	databases
MASTER_SITES=	MYSQL/Connector-C++

MAINTAINER=	ports@FreeBSD.org
COMMENT=	MySQL database connector for C++

LICENSE=	GPLv2 # only
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libboost_regex.so:devel/boost-libs

USE_MYSQL=	51+
USES=		cmake:outsource
USE_LDCONFIG=	yes
CMAKE_ARGS=	-DDOC_DESTINATION="${DOCSDIR}"

PLIST_SUB=	PORTVERSION=${PORTVERSION}

PORTDOCS=	*
OPTIONS_DEFINE=	DOCS

post-install:
	@${RM} -f ${STAGEDIR}${DOCSDIR}/INSTALL \
		${STAGEDIR}${DOCSDIR}/COPYING

.if defined(MAINTAINER_MODE)
CMAKE_ARGS+=	-DMYSQLCPPCONN_TEST_NOT_IMPLEMENTED:BOOL=1 \
		-DMYSQLCPPCONN_BUILD_EXAMPLES:BOOL=1
regression-test: build
#	These tests assume that a database is running on localhost,
#	with user:root and pass:root
	(cd ${WRKDIR}/.build ; \
	test/CJUnitTestsPort/CJUnitTestsPort --verbose ; \
	test/driver_test --verbose ; \
	test/static_test --verbose ; \
	examples/connect --verbose ; \
	examples/connection_meta_schemaobj --verbose ; \
	examples/debug --verbose ; \
	examples/dynamic_load --verbose ; \
	examples/exceptions --verbose ; \
	examples/prepared_statement --verbose ; \
	examples/resultset --verbose ; \
	examples/resultset_binary --verbose ; \
	examples/resultset_meta --verbose ; \
	examples/resultset_types --verbose ; \
	examples/statement --verbose ; \
	test/unit/classes/art_resultset --verbose ; \
	test/unit/classes/connection --verbose ; \
	test/unit/classes/databasemetadata --verbose ; \
	test/unit/classes/parametermetadata --verbose ; \
	test/unit/classes/preparedstatement --verbose ; \
	test/unit/classes/resultset --verbose ; \
	test/unit/classes/resultsetmetadata --verbose ; \
	test/unit/classes/savepoint --verbose ; \
	test/unit/classes/statement )
.endif

.include <bsd.port.mk>
