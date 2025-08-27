# 📘 Documentação de Troubleshooting em Redes  

## 1. Introdução  
Troubleshooting em redes é o processo sistemático de **identificar, diagnosticar e resolver problemas de conectividade, desempenho ou configuração** em ambientes de rede.  
Este documento fornece um guia de referência para lidar com incidentes comuns, boas práticas e métodos de análise.  

---

## 2. Abordagem Sistemática de Troubleshooting  

1. **Identificação do Problema**  
   - Recolher sintomas relatados pelos usuários.  
   - Verificar o escopo (um usuário, vários, toda a rede).  
   - Anotar mensagens de erro ou comportamentos anormais.  

2. **Definição do Escopo**  
   - O problema está em **camada física, lógica ou aplicação**?  
   - O impacto é **local, segmentado ou global**?  

3. **Hipóteses e Testes**  
   - Levantar possíveis causas.  
   - Testar uma hipótese de cada vez.  

4. **Implementação da Solução**  
   - Corrigir a falha com a menor intervenção possível.  
   - Registrar o que foi feito.  

5. **Validação e Monitoramento**  
   - Confirmar se a solução resolveu o problema.  
   - Monitorar para garantir estabilidade.  

---

## 3. Ferramentas Essenciais de Diagnóstico  

- **ping** → Testa conectividade básica entre hosts.  
- **traceroute / tracert** → Verifica o caminho percorrido pelos pacotes.  
- **ipconfig / ifconfig** → Exibe configuração de rede do host.  
- **nslookup / dig** → Testa resolução DNS.  
- **netstat** → Mostra conexões ativas e portas em uso.  
- **tcpdump / Wireshark** → Captura e analisa tráfego de rede.  
- **nmap** → Escaneia portas e serviços disponíveis.  

---

## 4. Troubleshooting por Camadas (Modelo OSI)  

### 🔹 Camada 1 – Física  
- **Sintomas:** Sem sinal, cabos desconectados, portas danificadas.  
- **Ações:**  
  - Verificar cabos, conectores e portas.  
  - Conferir LEDs dos switches/roteadores.  
  - Substituir cabos/testar em outra porta.  

### 🔹 Camada 2 – Enlace  
- **Sintomas:** Loops, colisões, problemas de VLAN.  
- **Ações:**  
  - Conferir tabelas ARP e MAC.  
  - Validar VLAN correta.  
  - Verificar spanning tree (STP).  

### 🔹 Camada 3 – Rede  
- **Sintomas:** Perda de pacotes, roteamento incorreto.  
- **Ações:**  
  - Testar conectividade com ping.  
  - Validar rotas com traceroute.  
  - Conferir tabelas de roteamento.  

### 🔹 Camada 4 – Transporte  
- **Sintomas:** Conexão instável, portas bloqueadas.  
- **Ações:**  
  - Verificar firewall e ACLs.  
  - Testar portas abertas (nmap/netstat).  

### 🔹 Camada 5 a 7 – Sessão, Apresentação e Aplicação  
- **Sintomas:** Aplicação inacessível, DNS não resolve nomes, serviços parados.  
- **Ações:**  
  - Conferir se o serviço está ativo (ex: web, e-mail).  
  - Validar resolução DNS.  
  - Checar logs da aplicação.  

---

## 5. Problemas Comuns e Soluções  

| Problema                        | Possível Causa                  | Solução                                                                 |
|---------------------------------|----------------------------------|-------------------------------------------------------------------------|
| Sem acesso à internet           | Cabo desconectado / DHCP falho  | Verificar conexão física e renovar IP.                                  |
| Rede lenta                      | Congestionamento / interferência | Monitorar tráfego, aplicar QoS, verificar largura de banda.             |
| DNS não resolve nomes           | Servidor DNS indisponível        | Testar nslookup, alterar DNS (ex: 8.8.8.8).                             |
| Queda intermitente              | Problemas no Wi-Fi / cabos ruins | Trocar canal Wi-Fi, testar cabeamento, substituir equipamentos defeituosos. |
| Porta/serviço inacessível       | Firewall bloqueando              | Revisar regras de firewall e ACLs.                                      |

---

## 6. Boas Práticas  

- Sempre começar do **mais simples para o mais complexo**.  
- Documentar sintomas, causas e soluções aplicadas.  
- Manter inventário atualizado de equipamentos e configurações.  
- Monitorar rede com ferramentas (Zabbix, PRTG, Nagios, Grafana).  
- Ter planos de contingência e redundância.  

---

## 7. Fluxo de Decisão Rápido  

```text
1. O dispositivo liga? → NÃO → verificar energia/cabos.
2. Tem link físico? (LEDs acesos) → NÃO → testar cabos/portas.
3. IP está correto? → NÃO → renovar DHCP/configurar manualmente.
4. Consegue pingar gateway? → NÃO → verificar roteador/switch.
5. Consegue pingar site externo por IP? → NÃO → verificar ISP.
6. DNS resolve nomes? → NÃO → alterar servidor DNS.
7. Aplicação funciona? → NÃO → verificar firewall/servidor.
