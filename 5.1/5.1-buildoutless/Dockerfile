FROM python:2.7-slim
RUN apt-get update && apt-get install -y gcc && rm -rf /var/lib/apt/lists/*
ADD requirements.txt /requirements.txt
RUN pip install -r requirements.txt && rm -fr /root/.cache
RUN useradd --system -m -d /plone -U -u 500 plone \
 && mkdir -p /data/filestorage /data/blobstorage /data/log\
 && chown -R plone:plone /data
RUN pip install collective.easyform
USER plone
RUN mkzopeinstance -d /plone -u admin:admin
COPY site.zcml /plone/etc/site.zcml
COPY zope.conf /plone/etc/zope.conf
VOLUME /data
#ENV Z3C_AUTOINCLUDE_DEPENDENCIES_DISABLED=1
#ENV Z3C_AUTOINCLUDE_PLUGINS_DISABLED=1
CMD /plone/bin/zopectl fg
USER root
