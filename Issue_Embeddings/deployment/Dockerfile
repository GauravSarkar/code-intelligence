# for https://cloud.docker.com/u/hamelsmu/repository/docker/hamelsmu/issuefeatures-api-cpu
#
# Building this image
#
# The context should be the root of the code-intelligence repository; this allows shared python code
# (i.e. code in py/ to be pulled in.)
FROM python:3.6-slim-stretch

RUN apt-get update 
RUN apt-get upgrade -y
RUN apt-get install --reinstall build-essential -y
RUN apt install -y gcc g++
RUN apt-get -y install cmake

# install large files first so that they are cached.
RUN pip install https://download.pytorch.org/whl/cpu/torch-1.1.0-cp36-cp36m-linux_x86_64.whl
RUN pip install https://download.pytorch.org/whl/cpu/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl
RUN pip install plac==0.9.6 fastai==1.0.53.post3 fastprogress==0.1.21 mdparse==0.13 spacy==2.1.4 numpy==1.16.4 \
    pandas==0.24.2 scikit-learn==0.20.3 scipy==1.2.1 matplotlib==3.0.3 jupyter-core==4.4.0

# hardcode some install so rebuilds are faster, because cannot cache requirements.txt
RUN pip install \
    appnope==0.1.0 \
    beautifulsoup4==4.7.1 \
    bs4==0.0.1 \
    flask==1.0.2 \
    flask-session==0.3.1 \
    ftfy==4.4.3 \
    # TODO(jlewi): Do we really need gcfs?
    gcsfs==0.2.1 \
    google-auth-oauthlib==0.3.0 \
    google-auth==1.6.3 \
    gunicorn==19.9.0 \
    html5lib==1.0.1 \
    idna==2.8 \
    ijson==2.3 \
    ipdb==0.12 \
    ipykernel==5.1.0 \
    ipython-genutils==0.2.0 \
    ipython==7.5.0 \
    mistune==0.8.4 \
    pillow==6.0.0 \
    pycparser==2.19 \
    six==1.12.0 \
    textacy==0.7.1 \
    tqdm==4.32.2 \
    widgetsnbextension==3.4.2

COPY Issue_Embeddings/flask_app flask_app/
# TODO(jlewi): Model should be downloaded at runtime; do we still need to make the directory in
# the docker file
RUN mkdir -p model_files

EXPOSE 80
CMD python app.py