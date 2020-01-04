# Naic_Reid_Docker

## Description

This project is to create running process for official reproduction of naic-reid project docker image.
Run Method

## step 1:Build from Dockerfile
```bash
git clone https://<username>:<password>@github.com/absorbguo/naic-reid-reproduce.git
cd naic-reid-reproduce
git clone https://<username>:<password>@github.com/absorbguo/naic-reid-rush-team.git
docker build -t reid:rush-team-unit-test --file Dockerfile.unit-test ./
docker build -t reid:rush-team-train --file Dockerfile.train ./
docker build -t reid:rush-team-test --file Dockerfile.test ./
docker build -t reid:rush-team-rerank --file Dockerfile.rerank ./
```

## step 2:Run Docker for unit test
`data_path`是本地数据所在地址。 `mount_data_path`是容器内部挂载的地址。

2 运行单元测试镜像。如果有最终生成文件`NAIC2019_unit_test.json`生成在answer文件夹中则通过测试。在挂载的根目录下会生成unit-test.log，通过该log进行确认。

```bash
nvidia-docker run --name reid-unit-test -d --rm -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-unit-test
```

ps:运行完单元测试后请删除model路径下的所有文件。

3 运行训练镜像。过程文件产生在`./model`中。在挂载的根目录下会生成train.log，通过该log进行确认。

## step 3:Run Docker for train
```bash
nvidia-docker run --name reid-train -d --rm -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-train
```

4 运行推理镜像。最终文件`NAIC2019_5rush_final.json`生成在answer文件夹。在挂载的根目录下会生成test.log，通过该log进行确认。

## step 4:Run Docker for test
```bash
nvidia-docker run --name reid-test -d --rm -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-test
```

5 如果第4步运行完后没有在answer文件夹下生成最终文件。运行rerank镜像。再次进行rerank，最终文件`NAIC2019_5rush_final.json`生成在answer文件夹。在挂载的根目录下会生成rerank.log，通过该log进行确认。

## step 5:Run Docker for rerank
```bash
nvidia-docker run --name reid-rerank -d --rm -v <data_path>:<mount_data_path> --shm-size=30720m reid:rush-team-rerank
```
