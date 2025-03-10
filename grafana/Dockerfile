FROM grafana/grafana:6.7.4

ENV GF_ANALYTICS_REPORTING_ENABLED=FALSE \
    GF_AUTH_ANONYMOUS_ENABLED=true \
    GF_AUTH_BASIC_ENABLED=false \
    GF_PATHS_PLUGINS="/var/lib/grafana-plugins" \
    GF_SECURITY_ADMIN_PASSWORD=admin \
    GF_SECURITY_ADMIN_USER=admin \
    GF_SECURITY_ALLOW_EMBEDDING=true \
    GF_SECURITY_DISABLE_GRAVATAR=true \
    GF_USERS_ALLOW_SIGN_UP=false \
    DATABASE_PORT=5432

USER root

RUN grafana-cli --pluginsDir "${GF_PATHS_PLUGINS}" plugins install pr0ps-trackmap-panel 2.1.0 && \
    grafana-cli --pluginsDir "${GF_PATHS_PLUGINS}" plugins install natel-discrete-panel 0.1.0 && \
    grafana-cli --pluginsDir "${GF_PATHS_PLUGINS}" plugins install grafana-piechart-panel 1.5.0 && \
    grafana-cli --pluginsDir "${GF_PATHS_PLUGINS}" --pluginUrl https://github.com/panodata/grafana-map-panel/releases/download/0.9.0/grafana-map-panel-0.9.0.zip plugins install grafana-worldmap-panel-ng

USER grafana

COPY datasource.yml /etc/grafana/provisioning/datasources/
COPY dashboards.yml /etc/grafana/provisioning/dashboards/
COPY dashboards/internal/*.json /dashboards_internal/
COPY dashboards/*.json /dashboards/

EXPOSE 3000
