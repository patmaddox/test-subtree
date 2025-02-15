PORTNAME=	palisade
DISTVERSIONPREFIX=	v
DISTVERSION=	1.11.9
CATEGORIES=	security math

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	PALISADE lattice cryptography library for Fully Homomorphic Encryption
WWW=		https://palisade-crypto.org

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

BROKEN_i386=		fails to build: a declaration of 'Mul128' must be available

BUILD_DEPENDS=	autoconf:devel/autoconf # possibly a mistake in the project

USES=		cmake:noninja,testing localbase # compiler:c++11-lang
USE_GITLAB=	yes
USE_GITHUB=	nodefault
GL_PROJECT=	palisade-release # there's also palisade-development
GL_TAGNAME=	3d1f9a3f9fd389df1f8f27f286511f4f5871258b
GH_TUPLE=	\
		JerryRyan:cereal:a384b101:cereal/third-party/cereal \
		google:benchmark:e451e50e:benchmark/third-party/google-benchmark \
		google:googletest:8b4817e3:google_test/third-party/google-test
USE_LDCONFIG=	yes

CMAKE_OFF=	BUILD_UNITTESTS BUILD_EXAMPLES BUILD_BENCHMARKS
CMAKE_OFF+=	WITH_NTL # https://gitlab.com/palisade/palisade-development/-/issues/180
CMAKE_ARGS=	-DWITH_NTL=Y # libntl.so will be discontinued in 1.11, see https://gitlab.com/palisade/palisade-development/-/issues/180
CMAKE_TESTING_ON=	BUILD_UNITTESTS
CMAKE_TESTING_TARGET=	testall

CXXFLAGS+=	-I${WRKSRC}/third-party/google-test/googletest

BINARY_ALIAS=	git=false

LDFLAGS+=	-pthread # only for tests: see https://gitlab.com/palisade/palisade-release/-/issues/23

OPTIONS_DEFINE=		OPENMP HEXL
.if exists(/usr/include/omp.h)
OPTIONS_DEFAULT=	OPENMP
.endif

HEXL_DESC=		Use Intel Hexl Library

OPENMP_CMAKE_BOOL=	WITH_OPENMP
HEXL_CMAKE_BOOL=	WITH_HEXL
HEXL_LIB_DEPENDS=	libhexl.so:security/hexl

.include <bsd.port.pre.mk>

.if ${OPSYS} == FreeBSD
CXXFLAGS+=	-Wno-error=unused-but-set-variable
.endif

.include <bsd.port.post.mk>
