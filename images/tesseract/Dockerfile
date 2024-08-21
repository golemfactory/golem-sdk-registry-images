FROM jitesoft/tesseract-ocr

VOLUME /golem/input /golem/output /golem/work
WORKDIR /golem/work

# Added to alleviate the current shortcoming of Golem storage implementation which requires a volume
# to be defined in order to access the storage on the provider
VOLUME /storage