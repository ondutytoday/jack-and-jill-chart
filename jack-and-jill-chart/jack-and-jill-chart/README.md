# jack-and-jill-chart

Мультикомпонентный Helm-чарт для приложения jack-and-jill.

## Установка
```bash
helm install jj ./jack-and-jill-chart \
  --namespace jj --create-namespace
```

## Конфигурация
- Глобальные параметры: `s3`, `kafka`, `topics`, `statsd`, `imagePullSecrets`
- Компоненты: `configurator`, `ucdservice`, `collector`, `discovery`, `notifier`, `stub`, `externalservicestub`, `pgadmin`
  - Для каждого: `enabled`, `replicaCount`, `image.repository`, `image.tag`, `service.port`, `ingress`, `ingress2`

### Пример overrides
```bash
helm install jj ./jack-and-jill-chart \
  --set kafka.brokers="kafka-1:9092,kafka-2:9092" \
  --set configurator.image.repository=ghcr.io/org/configurator \
  --set configurator.image.tag=1.0.0 \
  --set configurator.service.port=8888 \
  --set configurator.ingress.enabled=true \
  --set configurator.ingress.hosts[0].host=cfg.example.com \
  --set configurator.ingress.hosts[0].paths[0].path=/ \
  --set configurator.ingress.hosts[0].paths[0].backend.serviceName=cfg-svc \
  --set configurator.ingress.hosts[0].paths[0].backend.servicePort=8888
```