cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.SmokeSimulation -DperfSimulation=SmokeSimulation -DseedCount=20 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.LoadListSimulation -DperfSimulation=LoadListSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.LoadCrudSimulation -DperfSimulation=LoadCrudSimulation 2>&1 | grep -E "another performance run|Setup complete|Setup failed|Safety stop|Teardown of|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"

cd ~/dev/projects/test-automation && mvn gatling:test -Dgatling.simulationClass=com.example.tests.api.performance.simulations.LoadMixedSimulation -DperfSimulation=LoadMixedSimulation 2>&1 | grep -E "another performance run|Seeded|Setup complete|Setup failed|Safety stop|Deleted [0-9]|finished:|request count|percentile|mean response|BUILD"
