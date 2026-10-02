cd ~/dev/projects/test-automation && mvn test -DtestSuite=performance-unit.xml 2>&1 | grep -E "Tests run:|BUILD|FAIL"
