cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.SmokeSimulation -DperfSimulation=SmokeSimulation -DseedCount=20 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.LoadListSimulation -DperfSimulation=LoadListSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.LoadCrudSimulation -DperfSimulation=LoadCrudSimulation 2>&1 | grep -E "another performance run|Setup complete|Setup failed|Safety stop|Teardown of|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.LoadMixedSimulation -DperfSimulation=LoadMixedSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.StressListSimulation -DperfSimulation=StressListSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.StressGetSimulation -DperfSimulation=StressGetSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.StressCreateSimulation -DperfSimulation=StressCreateSimulation 2>&1 | grep -E "another performance run|Setup complete|Setup failed|Safety stop|Teardown of|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.StressUpdateSimulation -DperfSimulation=StressUpdateSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.StressDeleteSimulation -DperfSimulation=StressDeleteSimulation 2>&1 | grep -E "another performance run|Setup complete|Setup failed|Safety stop|Teardown of|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.StressMixedSimulation -DperfSimulation=StressMixedSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.SpikeMixedSimulation -DperfSimulation=SpikeMixedSimulation 2>&1 | grep -E "Seeded|Setup failed|Safety stop|p95 |Recovery check|Request failed|finished:|request count|percentile|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.SoakMixedSimulation -DperfSimulation=SoakMixedSimulation 2>&1 | grep -E "Seeded|Setup failed|Safety stop|p95 soak|Request failed|finished:|request count|percentile|BUILD"

Add performance test workflows (smoke, load, stress, spike, soak) and helper scripts

  # TEMPORARY - remove before merging: runs smoke with default settings on pushes to this branch
  push:
    branches: [your-feature-branch]
    paths:
      - ".github/workflows/performance-*.yml"
      - ".github/scripts/perf-*.sh"


      - name: TEMPORARY - network check (remove after diagnosis)
        env:
          TOKEN_SUBDOMAIN: ${{ secrets.AUTOMATION_PERFORMANCE_TEST_TOKEN_SUBDOMAIN }}
          PROXY: http://PROXY_HOST:8080
        run: |
          target="https://${TOKEN_SUBDOMAIN}.id.cyberark.cloud/"
          echo "Direct:"
          curl -sS -o /dev/null --max-time 20 -w "  HTTP %{http_code}\n" "$target" || echo "  failed"
          echo "Through the proxy:"
          curl -sS -o /dev/null --max-time 20 -x "$PROXY" -w "  HTTP %{http_code}\n" "$target" || echo "  failed"
          echo "Proxy-related environment variables on this worker:"
          env | grep -i -E '^(https?|no)_proxy=' | sed -E 's/=.*/=(set)/' || echo "  none"
