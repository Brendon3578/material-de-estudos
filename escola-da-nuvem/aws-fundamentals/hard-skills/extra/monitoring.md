# Monitoramento de recursos na AWS

O ato de **coletar, analisar e usar** dados para tomar decisões ou responder perguntas sobre a performance do sistema de TI é chamado de monitoramento.

Cada `datapoint` (ponto de dado) individual que um sistema cria é uma métrica. As métricas coletadas e analisadas ao longo do tempo se tornam **estatísticas**, como a utilização de CPU ao longo do tempo, mostrando um pico.

Recursos diferentes na **AWS** criam diferentes tipos de métricas sobre a sua **performance e atividade**. Saber a respeito delas pode auxiliar a planejar recursos mais escaláveis e com alta disponibilidade, antes mesmo que usuários finais enfrentam problemas de performance em horários de pico durante a execução da aplicação.

- Para o monitoramento de performance de recursos usa-se o **Amazon CloudWatch**, ele é usado para:
  - Detectar anomalias na aplicação.
  - Definir alarmes (**CloudWatch Alarms**) para avisar quando houver algo inesperado e tomar ações automatizadas com escalabilidade (como notificar alguém)
  - Visualizar e agrupar de forma centralizada logs (com Amazon CloudWatch Logs) e métricas com o Console através de **Dashboards**
  - Descobrir insights para manter a integridade das aplicações

## Organização do CloudWatch Logs

Os dados de log enviados para o CloudWatch Logs são organizados do seguinte modo:

- **Evento de log**: é um registro da atividade registrada pela aplicação ou recurso que está sendo monitorado, tendo um `date/time` carimbado e uma mensagem de evento.
- **Fluxo de log**: são sequências de eventos de log do mesmo recurso que está sendo monitorado.
- **Grupos de log**: agrupamento de fluxos de log que compartilham as mesmas configurações de retenção e permissões.

## Benefícios de monitoramento

- Responder a problemas operacionais de forma proativa antes que os **usuários finais percebam**
- Melhorar a **performance e a confiabilidade** de seus recursos
- Reconhecer **ameaças à segurança e eventos** sobre atividades suspeitas da utilização dos recursos e **Detectar** anomalias e picos de tráfego.
- Tomar decisões **orientadas por dados** para seu negócio
- Criar soluções mais **econômicas**
