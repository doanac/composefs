TEST_ASSETS_SMALL = \
	config.json.gz config-with-hard-link.json.gz special.json

TEST_ASSETS = ${TEST_ASSETS_SMALL} \
	cs9-x86_64-developer.json.gz cs9-x86_64-minimal.json.gz	\
	f36-x86_64-silverblue.json.gz

if ENABLE_VALGRIND
VALGRIND_PREFIX=libtool --mode=execute ${VALGRIND} --quiet --leak-check=yes --error-exitcode=42
endif

EXTRA_DIST = \
	gendir \
	dumpdir \
	test-lib.sh \
	test-units.sh \
	test-random-fuse.sh \
	test-checksums.sh \
	integration.sh \
	$(patsubst %,assets/%,${TEST_ASSETS_SMALL}) $(patsubst %,assets/%.sha256_erofs,${TEST_ASSETS_SMALL})

check-checksums:
	VALGRIND_PREFIX="${VALGRIND_PREFIX}" $(srcdir)/test-checksums.sh "$(builddir)/../tools/" "$(srcdir)/assets" "${TEST_ASSETS}"

check-units:
	VALGRIND_PREFIX="${VALGRIND_PREFIX}" $(srcdir)/test-units.sh "$(builddir)/../tools/"

check-random-fuse:
	VALGRIND_PREFIX="${VALGRIND_PREFIX}" $(srcdir)/test-random-fuse.sh "$(builddir)/../tools/"

check: check-units check-checksums check-random-fuse
