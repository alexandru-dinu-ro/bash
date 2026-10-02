cd ~/dev/projects/test-automation && mvn test -Dtest=ConnectivityCheckTest 2>&1 | grep -E "Connectivity check|Token initial|List policies|First policy|No policies|Tests run:|BUILD|ERROR|Exception"
