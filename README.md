cd ~/dev/projects/test-automation && mvn test -DtestSuite=performance-unit.xml 2>&1 | grep -E "Tests run:|BUILD|FAIL"

cd ~/dev/projects/test-automation && mvn test -Dtest=WriteCheckTest 2>&1 | grep -E "Write check|Created|Create of|Name search|Read back|Teardown|deleted:|Deleted|After teardown|delete failed|Tests run:|BUILD"
