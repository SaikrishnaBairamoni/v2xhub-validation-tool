# CARMA System Release Notes

## Version 4.13.0, released TBD

### Summary

The CARMA System 4.13.0 release includes the following significant updates:

- The CARLA-CARMA bridge in carma-carla-integration was migrated from ROS1 to ROS2 (Humble). Every bridge node — external objects, localization, vehicle status, odometry, Ackermann command, route, plugins, guidance, robot status, driver status — was ported from rospy to rclpy, with a new Docker build for the ROS2 stack.
- A new XML-RPC server and client pair was added to CDASim for the CARLA–MOSAIC bridge, replacing the original TraCI-based communication.
- CDASim's automated testing tooling was expanded with a PySide6 GUI, a scenario generator, and a scenario runner.
- carla-sensor-lib went through a CARLA 0.10.0 modernization pass, removing an old API workaround and adopting the new SemanticLidar API.
- cdasim-config picked up Town10 EVC configuration and a fix for the move-over-law lane-change scenario.

---

## Changes to Key Existing Repositories

### Carma Carla Integration

This release migrates the CARLA-CARMA ROS bridge from ROS1 to ROS2 (Humble) — the largest single piece of work in this release — and includes the CI/CD fixes needed to support the new ROS2 branch.

**Enhancements**

- **ROS1-to-ROS2 (Humble) bridge migration (CDAS-30, CDAS-31, CDAS-35, CDAS-44 through CDAS-50, CDAS-52 through CDAS-57, CDAS-61):** Ported the external objects, localization, vehicle status/info, odometry, Ackermann command (both directions), route, plugins, guidance, robot status, and driver status nodes from rospy to rclpy, including a new ament_python package structure and a Docker build for ROS2 Humble.
  * Pull Requests: [carma-carla-integration PR #81](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/81), [carma-carla-integration PR #84](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/84), [carma-carla-integration PR #85](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/85), [carma-carla-integration PR #86](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/86), [carma-carla-integration PR #87](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/87), [carma-carla-integration PR #88](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/88), [carma-carla-integration PR #93](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/93), [carma-carla-integration PR #94](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/94), [carma-carla-integration PR #95](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/95), [carma-carla-integration PR #96](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/96), [carma-carla-integration PR #97](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/97), [carma-carla-integration PR #98](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/98), [carma-carla-integration PR #99](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/99), [carma-carla-integration PR #100](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/100), [carma-carla-integration PR #101](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/101), [carma-carla-integration PR #102](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/102), [carma-carla-integration PR #104](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/104), [carma-carla-integration PR #105](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/105), [carma-carla-integration PR #106](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/106), [carma-carla-integration PR #108](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/108)

**Fixes**

- **ARC-248:** Fixed the Noetic build, which was relying on the new (ROS2 Humble) carma-base instead of the old one.
  * Pull Requests: [carma-carla-integration PR #78](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/78)
- [carma-carla-integration PR #103](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/103): Fixed CI/CD builds by including the develop-ros2 branch in GitHub Actions triggers (ci.yml, docker.yml, dockerhub.yml) and adding a suffix-replace argument that swaps `-ros2` for `-noetic`.
- [carma-carla-integration PR #113](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/113): Updated the Sonar workflow and renamed the properties file to `sonar-project.properties` to align with the shared `usdot-fhwa-stol/actions` sonar-scanner action.

**Other Updates**

- [carma-carla-integration PR #73](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/73), [carma-carla-integration PR #74](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/74), [carma-carla-integration PR #76](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/76): Post-4.5.0 release housekeeping — merged release/lavida into master, updated the `CARMA_VERSION` checkout variable, and synced develop to master.
- **ARC-205:** Renamed `j2735_msgs` and `j322_msgs` packages after they were merged into `j2735_v2x_msgs` and `j3224_v2x_msgs` in carma-msgs.
  * Pull Requests: [carma-carla-integration PR #77](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/77)
- **CDAS-62:** Integration testing of the carma-carla-bridge and carla-ros2-bridge against the CARMA platform and CARLA sim environment.
  * Pull Requests: [carma-carla-integration PR #109](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/109)
- **CDAS-83:** ROS2 migration Phase 2/3 integration testing.
  * Pull Requests: [carma-carla-integration PR #110](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/110), [carma-carla-integration PR #112](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/112)
- [carma-carla-integration PR #114](https://github.com/usdot-fhwa-stol/carma-carla-integration/pull/114): Merge ROS2 upgrade into develop.

### CDASim

**Enhancements**

- **CDAS-66 / CDAS-69:** New XML-RPC server and client implementation for the CARLA–MOSAIC bridge, replacing the original TraCI-based communication.
  * Pull Requests: [cdasim PR #251](https://github.com/usdot-fhwa-stol/cdasim/pull/251), [cdasim PR #252](https://github.com/usdot-fhwa-stol/cdasim/pull/252)
- **CDAS-65 — Initial GUI for Automated Testing Tool:** New PySide6 GUI for managing CDASim: browse a cdasim-config repository, select configurations, set up map/route files, pull Docker images, and build/start/stop simulations.
  * Pull Requests: [cdasim PR #250](https://github.com/usdot-fhwa-stol/cdasim/pull/250)
- **CDAS-43:** Scenario generator that produces deployment scripts (via YAML + Jinja2) for sequential Docker Compose simulation runs, removing manual setup.
  * Pull Requests: [cdasim PR #254](https://github.com/usdot-fhwa-stol/cdasim/pull/254)
- **CDAS-71:** Main automation script for CDASim's multi-scenario testing workflow: reads test cases from a YAML file, generates scenario-specific docker-compose files, runs each simulation, and collects outputs.
  * Pull Requests: [cdasim PR #257](https://github.com/usdot-fhwa-stol/cdasim/pull/257)
- **CDAS-34:** New scenario for UGA's ROS2 migration integration testing that excludes EVC-related configuration, since UGA doesn't have EVC access. Companion change: cdasim-config PR #35.
  * Pull Requests: [cdasim PR #248](https://github.com/usdot-fhwa-stol/cdasim/pull/248)
- **STRT-3:** Added a new training scenario.
  * Pull Requests: [cdasim PR #249](https://github.com/usdot-fhwa-stol/cdasim/pull/249)
- **CDAS-22:** Added a Town10 MOSAIC scenario to support ROS2 migration Phase 2 integration testing, ahead of the CARLA 0.10.0 upgrade.
  * Pull Requests: [cdasim PR #258](https://github.com/usdot-fhwa-stol/cdasim/pull/258)
- **CDAS-80:** Added a CARLA XML-RPC-based control path through the CarlaAmbassador/AbstractSumoAmbassador/CARLA XML-RPC server, enabling traffic-light sync through MOSAIC driven by either CARLA or SUMO.
  * Pull Requests: [cdasim PR #256](https://github.com/usdot-fhwa-stol/cdasim/pull/256)
- **CDAS-101:** Added Docker-in-Docker support so CDASim (Ubuntu 18.04) can launch the upgraded NS-3 Federate (Ubuntu 22.04 + 5G NR) inside its own container via MOSAIC's `DockerFederateExecutor`.
  * Pull Requests: [cdasim PR #262](https://github.com/usdot-fhwa-stol/cdasim/pull/262)
- **CDAS-87:** Added new log sources for data collection.
  * Pull Requests: [cdasim PR #263](https://github.com/usdot-fhwa-stol/cdasim/pull/263)

**Fixes**

- **CDAS-98:** Fixed vehicles "jumping" (visible vertical oscillation) when SUMO-controlled vehicles are mapped into the CARLA 3D world during CARLA–SUMO co-simulation via MOSAIC.
  * Pull Requests: [cdasim PR #261](https://github.com/usdot-fhwa-stol/cdasim/pull/261)
- **CDAS-79:** Fixed a CARLA version conflict by enabling CARLA to launch via the official CARLA Docker image in a Docker-in-Docker setup, since CDASim itself runs in a container.
  * Pull Requests: [cdasim PR #255](https://github.com/usdot-fhwa-stol/cdasim/pull/255)
- **SIM-31:** Fixed a bug where a CARMA vehicle's SUMO position was getting an offset applied twice; the CARMA vehicle is now filtered out of that step in the SUMO ambassador. Root cause still needs follow-up.
  * Pull Requests: [cdasim PR #271](https://github.com/usdot-fhwa-stol/cdasim/pull/271)

**Other Updates**

- **CDAS-23:** Finalized the SUMO network configuration for the Town10 map so the traffic light system is correctly synchronized with CARLA for co-simulation stability.
  * Pull Requests: [cdasim PR #259](https://github.com/usdot-fhwa-stol/cdasim/pull/259)
- [cdasim PR #264](https://github.com/usdot-fhwa-stol/cdasim/pull/264), [cdasim PR #260](https://github.com/usdot-fhwa-stol/cdasim/pull/260): ROS2 migration Phase 2/3 integration testing.
- [cdasim PR #266](https://github.com/usdot-fhwa-stol/cdasim/pull/266): Merge ROS2 upgrade into develop.
- [cdasim PR #267](https://github.com/usdot-fhwa-stol/cdasim/pull/267): Removed the ns3 docker setup from the docker build.
- [cdasim PR #269](https://github.com/usdot-fhwa-stol/cdasim/pull/269): Updated CARMA Messenger to support a new test plan.

### Cdasim Config

This release adds Town10 EVC configuration and a new GitHub Actions-based Docker build pipeline, alongside a fix for the move-over-law lane-change scenario.

**Enhancements**

- **CDAS-34:** New scenario for UGA's ROS2 migration integration testing that excludes EVC-related configuration, since UGA doesn't have EVC access. Companion change: cdasim PR #248.
  * Pull Requests: [cdasim-config PR #35](https://github.com/usdot-fhwa-stol/cdasim-config/pull/35)
- **STRT-3:** New CARMA training scenario. Companion change: cdasim PR #249.
  * Pull Requests: [cdasim-config PR #38](https://github.com/usdot-fhwa-stol/cdasim-config/pull/38)
- **ARC-175:** Enabled conditional toggling of cooperative perception (CP) multi-object tracking — on by default only for the use case that has SDSM, off elsewhere. Also updated ROS-related scenario configuration for the ROS2 Humble upgrade. Supports carma-platform PR #2517.
  * Pull Requests: [cdasim-config PR #4](https://github.com/usdot-fhwa-stol/cdasim-config/pull/4)
- [cdasim-config PR #45](https://github.com/usdot-fhwa-stol/cdasim-config/pull/45): Added a training scenario and volume to CDASim for training use.
- [cdasim-config PR #33](https://github.com/usdot-fhwa-stol/cdasim-config/pull/33): Brought the development folder up to date with ROS2 (Humble upgrade work), removed extra folders.
- [cdasim-config PR #54](https://github.com/usdot-fhwa-stol/cdasim-config/pull/54): Added a new loop route.

**Fixes**

- [cdasim-config PR #57](https://github.com/usdot-fhwa-stol/cdasim-config/pull/57): Fixed the move-over-law scenario in Town10 by correcting lanelet linestring/buffer configuration so all expected lane-change areas are properly marked.
- [cdasim-config PR #42](https://github.com/usdot-fhwa-stol/cdasim-config/pull/42): Fixed an abnormal trajectory issue affecting AWS-deployed instances.
- **CAR-6128:** Fixed the Google Maps API key for the UI; the key was previously exposed directly and wasn't working, the new key is now pulled from a private repo.
  * Pull Requests: [cdasim-config PR #36](https://github.com/usdot-fhwa-stol/cdasim-config/pull/36)

**Other Updates**

- [cdasim-config PR #51](https://github.com/usdot-fhwa-stol/cdasim-config/pull/51), [cdasim-config PR #49](https://github.com/usdot-fhwa-stol/cdasim-config/pull/49): Replaced Docker Hub automated builds with GitHub Actions Docker builds for xil-town10 and for cdasim-config generally.
- **CDAS-122:** Updated EVC config, docker compose file, and `localhost.sql` for Town10.
  * Pull Requests: [cdasim-config PR #53](https://github.com/usdot-fhwa-stol/cdasim-config/pull/53)
- [cdasim-config PR #52](https://github.com/usdot-fhwa-stol/cdasim-config/pull/52): Updated docker-compose configuration.
- [cdasim-config PR #56](https://github.com/usdot-fhwa-stol/cdasim-config/pull/56): Updated CARMA Messenger configuration settings to support an updated test plan.
- **TT-174:** Updated the README with instructions for placing and using the PyEOS bundle file in EVC-SUMO.
  * Pull Requests: [cdasim-config PR #5](https://github.com/usdot-fhwa-stol/cdasim-config/pull/5)
- [cdasim-config PR #46](https://github.com/usdot-fhwa-stol/cdasim-config/pull/46), [cdasim-config PR #48](https://github.com/usdot-fhwa-stol/cdasim-config/pull/48): ROS2 migration Phase 2/3 integration testing.
- [cdasim-config PR #50](https://github.com/usdot-fhwa-stol/cdasim-config/pull/50): Merge ROS2 upgrade into develop.

### Carma NS3 Adapter

**Enhancements**

- **CDAS-74:** Added support for a global parameter override YAML file in carma-config, so map- or scenario-specific parameter overrides can be version-controlled.
  * Pull Requests: [carma-ns3-adapter PR #35](https://github.com/usdot-fhwa-stol/carma-ns3-adapter/pull/35)
- **CDAS-38:** Added a new registration sender script.
  * Pull Requests: [carma-ns3-adapter PR #36](https://github.com/usdot-fhwa-stol/carma-ns3-adapter/pull/36)

### Carla Sensor Lib

**Enhancements**

- **CDAS-70 — Carla Sensor Lib Carla 0.10.0 Modernization:** Removed the y-axis negation workaround that was needed for the old API, replaced the deprecated `upper_fov`/`lower_fov` attributes with `horizontal_fov`, and adopted the new `carla.SemanticLidar` API.
  * Pull Requests: [carla-sensor-lib PR #22](https://github.com/usdot-fhwa-stol/carla-sensor-lib/pull/22)

**Other Updates**

- [carla-sensor-lib PR #24](https://github.com/usdot-fhwa-stol/carla-sensor-lib/pull/24): Updated docker network configuration and removed an unsafe logging call ahead of phase 3 network testing, and added CARLA 0.10.0 configuration support.
