# Example of using Flink within Docker

Just a quick example of creating a HA enabled Flink Cluster using Zookeeper within docker, being able to scale, and modify the local config.

This was created for a particular task, and is **not** recommended for prod.

## How to run

Launch a cluster in the background

`$ docker-compose up -d`

```bash
$ docker-compose up -d
[+] Running 11/11
 ✔ zookeeper-3 Pulled                                                                                                                                                            12.4s
 ✔ zookeeper-1 Pulled                                                                                                                                                            12.4s
 ✔ zookeeper-2 8 layers [⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                                                                                        12.4s
   ✔ b2ddfd337773 Pull complete                                                                                                                                                   7.3s
   ✔ 35794a35c4aa Pull complete                                                                                                                                                   7.8s
   ✔ 261269474501 Pull complete                                                                                                                                                   9.5s
   ✔ 48a873c16c38 Pull complete                                                                                                                                                   9.5s
   ✔ 91bcf425c56c Pull complete                                                                                                                                                   9.5s
   ✔ 71c2395ae368 Pull complete                                                                                                                                                   9.7s
   ✔ d47582dce413 Pull complete                                                                                                                                                  10.0s
   ✔ aa4ffe819d32 Pull complete                                                                                                                                                  10.0s
[+] Building 41.7s (6/6) FINISHED
 => [internal] load build definition from Dockerfile.flink                                                                                                                        0.0s
 => => transferring dockerfile: 152B                                                                                                                                              0.0s
 => [internal] load .dockerignore                                                                                                                                                 0.0s
 => => transferring context: 2B                                                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/flink:latest                                                                                                                   1.6s
 => [1/2] FROM docker.io/library/flink:latest@sha256:92f54911fe0cca9bcc140927db41494701033c42063b8ebd515a1664722e7e52                                                            39.3s
 => => resolve docker.io/library/flink:latest@sha256:92f54911fe0cca9bcc140927db41494701033c42063b8ebd515a1664722e7e52                                                             0.0s
 => => sha256:b21523e1b88827f5ecc352bf974b18f30cf5128f8c4aa18e24d30d8902fb56fe 835.39kB / 835.39kB                                                                                0.4s
 => => sha256:9515d8cfac64535163ef6cf6894a606752453c8b4ef7333792647fa5b4463360 4.65kB / 4.65kB                                                                                    0.8s
 => => sha256:92f54911fe0cca9bcc140927db41494701033c42063b8ebd515a1664722e7e52 549B / 549B                                                                                        0.0s
 => => sha256:c929cbfacdbc439040ca6a1cca5dfd67be13c7cce04d8f5d291b27c72abbce98 11.67kB / 11.67kB                                                                                  0.0s
 => => sha256:bf7211e5444e6bbc75cf67be4f2e77f5f153adf5a5689823d469b4fd2cb35ceb 4.50MB / 4.50MB                                                                                    1.0s
 => => sha256:d4f5624a09d669d2412f4d4faaa34210742169c99fed00f6d7d4b3bca537bb15 2.42kB / 2.42kB                                                                                    0.0s
 => => sha256:1b09e65e4944b6b9f2332392e3e7c431f313887ca2df6b563d687a225bd12c6c 148B / 148B                                                                                        0.5s
 => => sha256:23ba3f65a2a13dd0a05b4bcbdcf135b7fb2a5ecf02bb27a68ec9d58700785b50 469.99MB / 469.99MB                                                                               34.4s
 => => sha256:98ab336888995d1eba36437d2912a6985926cae9f873fe78695d8a76f892de47 2.11kB / 2.11kB                                                                                    1.0s
 => => extracting sha256:bf7211e5444e6bbc75cf67be4f2e77f5f153adf5a5689823d469b4fd2cb35ceb                                                                                         0.1s
 => => extracting sha256:b21523e1b88827f5ecc352bf974b18f30cf5128f8c4aa18e24d30d8902fb56fe                                                                                         0.0s
 => => extracting sha256:9515d8cfac64535163ef6cf6894a606752453c8b4ef7333792647fa5b4463360                                                                                         0.0s
 => => extracting sha256:1b09e65e4944b6b9f2332392e3e7c431f313887ca2df6b563d687a225bd12c6c                                                                                         0.0s
 => => extracting sha256:23ba3f65a2a13dd0a05b4bcbdcf135b7fb2a5ecf02bb27a68ec9d58700785b50                                                                                         4.7s
 => => extracting sha256:98ab336888995d1eba36437d2912a6985926cae9f873fe78695d8a76f892de47                                                                                         0.0s
 => [2/2] RUN mkdir -p /opt/flink/nfs && chown -R flink:flink /opt/flink/nfs                                                                                                      0.6s
 => exporting to image                                                                                                                                                            0.1s
 => => exporting layers                                                                                                                                                           0.1s
 => => writing image sha256:da928f5857c039c43b30912cbf3b9cc1fa9fff2c01f5ed456b8256734f95f206                                                                                      0.0s
 => => naming to docker.io/library/docker_flink-jobmanager                                                                                                                        0.0s
[+] Building 0.4s (6/6) FINISHED
 => [internal] load build definition from Dockerfile.flink                                                                                                                        0.0s
 => => transferring dockerfile: 37B                                                                                                                                               0.0s
 => [internal] load .dockerignore                                                                                                                                                 0.0s
 => => transferring context: 2B                                                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/flink:latest                                                                                                                   0.3s
 => [1/2] FROM docker.io/library/flink:latest@sha256:92f54911fe0cca9bcc140927db41494701033c42063b8ebd515a1664722e7e52                                                             0.0s
 => CACHED [2/2] RUN mkdir -p /opt/flink/nfs && chown -R flink:flink /opt/flink/nfs                                                                                               0.0s
 => exporting to image                                                                                                                                                            0.0s
 => => exporting layers                                                                                                                                                           0.0s
 => => writing image sha256:d9b1646c2ed4dec561f9fb7c8742a5807212304b2545cac3982b8d07d04aed24                                                                                      0.0s
 => => naming to docker.io/library/docker_flink-taskmanager                                                                                                                       0.0s
[+] Running 7/7
 ✔ Network docker_flink_backend          Created                                                                                                                                  0.0s
 ✔ Container docker_flink-jobmanager-1   Started                                                                                                                                  0.8s
 ✔ Container docker_flink-zookeeper-1-1  Started                                                                                                                                  1.2s
 ✔ Container docker_flink-zookeeper-2-1  Started                                                                                                                                  0.8s
 ✔ Container docker_flink-zookeeper-3-1  Started                                                                                                                                  1.1s
 ✔ Container docker_flink-taskmanager-2  Started                                                                                                                                  1.2s
 ✔ Container docker_flink-taskmanager-1  Started                                                                                                                                  1.6s
```

Scale the cluster up or down to N TaskManagers

`$ docker-compose up -d --scale taskmanager=<N>`

```bash
$ docker-compose up -d --scale taskmanager=4
[+] Running 8/8
 ✔ Container docker_flink-jobmanager-1   Running                                                                                                                                  0.0s
 ✔ Container docker_flink-zookeeper-2-1  Running                                                                                                                                  0.0s
 ✔ Container docker_flink-zookeeper-3-1  Running                                                                                                                                  0.0s
 ✔ Container docker_flink-zookeeper-1-1  Running                                                                                                                                  0.0s
 ✔ Container docker_flink-taskmanager-2  Running                                                                                                                                  0.0s
 ✔ Container docker_flink-taskmanager-1  Running                                                                                                                                  0.0s
 ✔ Container docker_flink-taskmanager-4  Started                                                                                                                                  1.0s
 ✔ Container docker_flink-taskmanager-3  Started                                                                                                                                  0.6s
```

Access the JobManager container

`$ docker exec -it $(docker ps --filter name=docker_flink-jobmanager-1 --format={{.ID}}) /bin/bash`

`$ docker exec -it $(docker ps --filter name=docker_flink-taskmanager-1 --format={{.ID}}) /bin/bash`

`$ docker exec -it $(docker ps --filter name=docker_flink-taskmanager-2 --format={{.ID}}) /bin/bash`

`$ docker exec -it $(docker ps --filter name=docker_flink-zookeeper-1 --format={{.ID}}) /bin/bash`

`$ docker exec -it $(docker ps --filter name=docker_flink-zookeeper-2 --format={{.ID}}) /bin/bash`

`$ docker exec -it $(docker ps --filter name=docker_flink-zookeeper-3 --format={{.ID}}) /bin/bash`

Kill the cluster

`$ docker-compose down`

Access Web UI

When the cluster is running, you can visit the web UI at http://localhost:8081.

## Notes

This will not be maintained/improved on.
