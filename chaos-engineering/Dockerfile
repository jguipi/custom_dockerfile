FROM python:3.10.2-alpine

ENV PATH=/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG=C.UTF-8
ENV PYTHON_VERSION=3.10.2
ENV PYTHON_PIP_VERSION=21.3.1
ENV CHAOSTOOLKIT_VERSION=1.11.0

RUN apk add --no-cache --virtual build-deps gcc g++ git libffi-dev linux-headers \
        python3-dev musl-dev && \
    pip install --no-cache-dir -q -U pip setuptools && \
    pip install --no-cache-dir chaostoolkit=="${CHAOSTOOLKIT_VERSION}" && \
    pip install --no-cache-dir chaostoolkit-kubernetes && \
    pip install --no-cache-dir chaostoolkit-lib[jsonpath] && \
    apk del build-deps

RUN addgroup --gid 1001 svc
RUN adduser --disabled-password --home /home/svc --uid 1001 --ingroup svc svc
WORKDIR /home/svc

USER 1001

ENTRYPOINT ["/usr/local/bin/chaos"]
CMD ["--help"]
