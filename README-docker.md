# How to build your docker containers for Crop-filling

Requirements:

- Miniconda installer: [Miniconda3-py38_4.12.0-Linux-x86_64.sh](https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh)
- FreeSurfer 7 development version: `freesurfer-linux-ubuntu18_x86_64-7-dev.tar.gz`

1. Change into repo directory (after cloning, obviously)
```
cd /path/to/CODEC_Crop-Filling
```

2. Change into FreeSurfer container directory and download Dockerfile requirements:
   - MiniConda installer (takes seconds)
   - FreeSurfer v7-dev, ubuntu 18 (takes minutes to hours, depending on your connection)
```
cd FS_dev
wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh
wget https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/dev/freesurfer-linux-ubuntu18_x86_64-7-dev.tar.gz
```

3. Build FreeSurfer docker container
```
DOCKERTAG=noxtoby/cropfilling:fs7dev
docker build --progress=plain --tag ${DOCKERTAG} -f Dockerfile .
```

4. Save IMAGE ID to FreeSurfer image
```
docker images ${DOCKERTAG}
# Manually copy the IMAGE ID and assign an environment variable
IMAGEID=af2a88f3f32d
```

5. Build Crop-filling container
```
cd ../crop_fill
DOCKERTAGCF=noxtoby/cropfilling:crop_fill
docker build --progress=plain --tag ${DOCKERTAGCF} -f Dockerfile .
```
