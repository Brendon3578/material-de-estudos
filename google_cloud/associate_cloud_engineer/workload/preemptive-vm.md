# VM preemptivas

São instâncias que estão disponíveis por um preço muito baixo (60% a 91% de desconto). Mas essas VMS podem ser interrompidas pelo Compute Engine caso precisa recuperar a capacidade de computação para alocação em outras VMs.

Se o seu app for tolerante falha, poderá reduzir consideravelmente os custos do Compute Engine. Exemplo: jobs de processamento em lote (batch)

## Limitações

- O Compute Engine pode interromper as instâncias a qualquer momento devido a eventos do sistema.
- O Compute Engine sempre interrompe VMS que estão em execução a mais de 24 horas.
- São recursos finitos do Compute Engine (nem sempre estão disponíveis)
- São excluídas do SLA do Compute Engine

## Boas práticas

- É recomendado a criação em **massa de VMS**
- Usar formas menores de máquina
- Executar grandes clusters de VM preemptiva fora dos horários de pico
- Desenvolver APPs para serem tolerantes a falhas e preempção
- Criar scrips de desligamentos para salvar o progresso do trabalho.
