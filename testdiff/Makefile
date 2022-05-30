
TEST_REGRESS := ../repo/test_regress

SNAPSHOT := ./snapshot

IGNORE_SUFFIX := .status .log .dat .d .o .a .so .txt .html .includecache \
                 .out .vcd .fst .tree .dot .csv .xml .hash .cmake

diff: diff-vlt diff-vltmt diff-dist

diff-%:
	(icdiff -N --recursive $(SNAPSHOT)/obj_$* $(TEST_REGRESS)/obj_$* | grep -v "Only in $(TEST_REGRESS)" ; true)

snap: snap-vlt snap-vltmt snap-dist

snap-%:
	rm -rf $(SNAPSHOT)/obj_$*
	mkdir -p $(SNAPSHOT)/obj_$*
	cp -r $(TEST_REGRESS)/obj_$* $(SNAPSHOT)/
	for suffix in $(IGNORE_SUFFIX); do \
    find $(SNAPSHOT)/obj_$* -name "*$$suffix" | xargs -r rm; \
  done
	find $(SNAPSHOT)/obj_$* -name "gmon.out.*" | xargs -r rm
	find $(SNAPSHOT)/obj_$* -wholename "*/CMakeFiles/Makefile2" | xargs -r rm
	find $(SNAPSHOT)/obj_$* -type f -executable | xargs -r rm
