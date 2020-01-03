#Naic_Reid_Docker

##Description

This project is to create running process for official reproduction of naic-reid project docker image.
Run Method

##step 1:Build from Dockerfile
```bash
git clone https://<username>:<password>@github.com/absorbguo/naic-reid-reproduce
cd naic-reid-reproduce
git clone https://<username>:<password>@github.com/absorbguo/naic-reid-rush-team.git
docker build -t reid:rush-team-train --file Dockerfile.train ./
docker build -t reid:rush-team-test --file Dockerfile.test ./
```

##step 2:Run Docker for train
```bash
nvidia-docker run --name reid-train -d -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-train
```

##step 3:Run Docker for test
```bash
nvidia-docker run --name reid-test -d -v <data_path>:<mount_data_path> --shm-size=20480m reid:rush-team-test
```
