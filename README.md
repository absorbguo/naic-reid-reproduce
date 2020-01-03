Naic_Reid_Docker

Description

This project is to create running process for official reproduction of naic-reid project docker image.
Run Method

Build from Dockerfile

git clone https://<username>:<password>@github.com/absorbguo/naic-reid-reproduce
cd naic-reid-reproduce
git clone https://<username>:<password>@github.com/absorbguo/naic-reid-rush-team.git
docker build -t reid:rush-team-train --file Dockerfile.train ./
docker build -t reid:rush-team-test --file Dockerfile.test ./

Run Docker for train

nvidia-docker run --name reid-train -d -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-train


Run Docker for test

nvidia-docker run --name reid-test -d -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-test

