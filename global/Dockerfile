FROM sasfdacr.azurecr.io/viya-4-x64_oci_linux_2-docker/sas-decisions-runtime-components:1.150.15-20260911.1789149876169 AS base
FROM sasfdacr.azurecr.io/viya-4-x64_oci_linux_2-docker/sas-decisions-runtime-base:1.150.15-20260911.1789149883547
LABEL model="container image"
ENV SAS_SCR_APP_PATH=/global
USER sas
USER root
COPY --from=base /python311 /python
RUN rpm -i --force /python/*.rpm && rm -r /python
ENV MAS_PYPATH=/usr/bin/python3.11
USER sas
COPY --from=base  /fraud /
COPY --from=base  /hiredis /
COPY --from=base  /kafka /
COPY --from=base  /oracle /
ENV ORACLE_HOME=/usr/lib/oracle/23/client64 ORAENV_ASK=NO SASORA=V9 TWO_TASK=ORACLE_SID
ENV LD_LIBRARY_PATH=/opt/scr/viya/home/SASFoundation/utilities/bin:/opt/scr/viya/home/SASFoundation/sasexe:/usr/lib64:/usr/lib/oracle/23/client64/lib
COPY --chown=sas:sas unzipped/ /modules/
COPY --chown=sas:sas manifest/ /manifest/
