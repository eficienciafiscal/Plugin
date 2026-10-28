# Eficiência Fiscal para Claude

Consulte documentos fiscais, CNDs e notificações DET/Fisconforme dos participantes autorizados na Eficiência Fiscal diretamente pelo Claude. O plugin reúne a conexão MCP e a habilidade `consultar-ef`, que orienta a seleção dos participantes, as consultas e a interpretação dos dados disponíveis. Quando habilitado, também permite preparar solicitações de contato e enviá-las após sua confirmação.

**Site:** https://eficienciafiscal.com.br/  
**Servidor MCP:** https://eficiencia.app/mcp  
**Suporte:** software@eficienciafiscal.com.br

## O que você pode consultar

| Recurso | Dados disponíveis conforme a conexão e o documento |
| --- | --- |
| Participantes | Empresas autorizadas e regimes tributários cadastrados, com data de referência e vigência. |
| Documentos fiscais | Pesquisas separadas de NF-e, NFC-e, NFS-e, CT-e, MDF-e e NFCom, por participante, período e papel na operação. |
| Detalhes | Identificação, partes, situação e valores retornados pelas ferramentas de cada tipo de documento. |
| Itens de NF-e e NFC-e | Produtos, quantidades, unidades, valores e campos fiscais disponíveis. |
| Pagamentos de NF-e e NFC-e | Pagamentos declarados, códigos dos meios de pagamento e respectivas descrições, quando disponíveis. |
| Tributação | Parâmetros cadastrados de ICMS e PIS/COFINS por participante e vigência. |
| CNDs | Certidões e consultas por esfera, nome, validade, situação e orientação disponíveis, além do arquivo original em PDF ou HTML quando autorizado. |
| DET da SEFIN/RO | Listagem de notificações por participante e período, com código, título, datas e status. |
| Fisconforme da SEFIN/RO | Notificações por participante e competência, com descrição, situação e detalhe disponível, incluindo inconsistência, justificativa e referências documentais. |
| Contato com a EF | Preparação de solicitações, anexos autorizados e envio após revisão e confirmação explícita do usuário. |
| Consumo | Uso e plano do acesso selecionado. |

A disponibilidade depende das ferramentas habilitadas no servidor, das permissões da conexão e dos dados existentes. Instalar o plugin não habilita novos acessos nem garante que todos os campos estejam preenchidos.

O MCP entrega dados para o Claude analisar. Cálculos, comparações e sínteses são feitos pelo assistente a partir dos resultados, respeitando as limitações informadas.

## Pré-requisitos

- Conta ativa na Eficiência Fiscal, com MCP habilitado para o escritório.
- Usuário com permissão de consulta aos participantes desejados.
- Licenças e permissões dos módulos que deseja consultar. A autorização de um participante não libera automaticamente todos os módulos.
- Conta Claude com suporte a plugins e conectores, conforme o plano e as políticas da organização.
- Documentos disponíveis para os participantes e períodos consultados.

Não é necessário usar uma conta de administrador para consultar os dados.

## Instalação e conexão

1. No Claude, abra **Personalizar → Plugins** e use a opção de importar um plugin para selecionar o ZIP fornecido pela Eficiência Fiscal.
2. Abra o plugin instalado e inicie a conexão com o servidor MCP da Eficiência Fiscal.
3. Na página de login da EF, entre com seu usuário e revise os participantes antes de autorizar o acesso.
4. Volte ao Claude e peça: **“Liste os participantes autorizados na minha conexão com a Eficiência Fiscal.”**

A autenticação utiliza OAuth com CIMD, permitindo que o Claude apresente sua identidade ao servidor. No fluxo do Claude web, não é necessário informar manualmente Client ID ou segredo. Digite sua senha somente na página de login da EF, nunca na conversa.

Os nomes dos controles podem variar conforme a versão e o idioma do Claude. Consulte também as [instruções oficiais de instalação de plugins](https://support.claude.com/en/articles/13837440-use-plugins-in-claude).

## Exemplos de uso

Substitua os campos entre colchetes por dados de um participante autorizado.

**Identificar os participantes disponíveis**

> Liste os participantes autorizados na minha conexão, mostrando nome e CNPJ.

**Conferir documentos recebidos**

> Consulte as NF-e recebidas pelo participante [CNPJ] entre [data inicial] e [data final]. Mostre número, fornecedor, valor total e situação disponível. Informe se o resultado estiver parcial.

**Consultar itens e pagamentos de uma nota**

> Localize a NF-e número [número], série [série], recebida pelo participante [CNPJ] em [data]. Mostre seus itens e pagamentos declarados, incluindo descontos e troco quando disponíveis.

**Conferir CNDs**

> Consulte as CNDs disponíveis do participante [CNPJ]. Mostre esfera, nome, situação, validade e orientação. Identifique as vencidas com base nos dados retornados.

> Obtenha o arquivo da certidão [nome] que apareceu nessa consulta, no formato original disponível.

**Acompanhar notificações DET**

> Liste as notificações DET do participante [CNPJ] entre [data inicial] e [data final], mostrando título, data e status. Informe se existem páginas restantes.

**Consultar Fisconforme**

> Liste as notificações Fisconforme do participante [CNPJ] na competência [AAAA-MM]. Depois, mostre o detalhe da notificação [código], com a inconsistência e as referências disponíveis.

**Preparar contato com a EF**

> Prepare uma solicitação de ajuda sobre [módulo] para o participante [CNPJ], descrevendo [problema]. Mostre o conteúdo para minha revisão antes de enviar.

## CNDs, DET e Fisconforme

### CNDs

`consultar_cnds` consulta os dados já disponíveis na EF, com classificação Federal, Estadual, Municipal e Consulta. `obter_arquivo_cnd` entrega um arquivo indicado nessa listagem, em PDF ou HTML conforme o original.

A consulta não solicita emissão nem renovação de certidões. Uma certidão vencida ou uma falha de consulta ao portal não comprova dívida. Baixar um arquivo antigo não atualiza sua validade.

### DET

`listar_notificacoes_det` lista os dados das notificações já disponíveis na EF. O conteúdo, os PDFs e os anexos devem ser visualizados no portal da Eficiência Fiscal. A consulta MCP não registra ciência nem marca notificações como lidas.

### Fisconforme

`listar_fisconforme` pesquisa notificações por competência; `consultar_fisconforme` detalha uma notificação retornada pela listagem. Descrições, status, inconsistências, justificativas e dados associados são apresentados quando disponíveis.

Chaves de notas citadas na notificação são referências. Consultar essas notas exige uma chamada fiscal separada, mantendo o participante autorizado e respeitando as permissões e os créditos correspondentes. A consulta não apresenta defesa, contesta nem resolve notificações.

### Contato

Quando as ferramentas de contato estiverem disponíveis, o Claude pode preparar um rascunho e anexar até dois prints autorizados. O participante, o motivo, a descrição e os anexos devem ser revisados e confirmados pelo usuário antes do envio. Preparar um rascunho não significa abrir um chamado.

O contato não contrata módulos, não libera acesso a dados e não renova certidões. Havendo um chamado em aberto ou um intervalo de espera, o assistente deve respeitar o bloqueio e orientar o acompanhamento do atendimento existente.

## Limites e interpretação

- As pesquisas usam períodos de até 31 dias e paginação. Períodos maiores exigem consultas separadas.
- Cada página fiscal concluída consome um crédito, inclusive quando não encontra documentos. Itens e pagamentos têm paginação própria; detalhes e consultas de tributação concluídos também consomem um crédito. A medição de créditos não implica, por si só, cobrança financeira.
- A consulta de CNDs consome um crédito; cada arquivo entregue consome mais um. Cada página de DET ou Fisconforme e cada detalhe de Fisconforme concluído consomem um crédito.
- As chamadas são feitas para um participante autorizado por vez. Pedidos sobre vários CNPJs exigem chamadas separadas, com os resultados identificados por participante.
- As consultas fiscais devem ser sequenciais. Ao receber uma limitação, o assistente deve respeitar o tempo de espera informado pelo servidor.
- Dados ausentes ou pendentes não equivalem a zero. Uma resposta parcial não deve ser apresentada como resultado completo.
- Pagamentos declarados não comprovam liquidação bancária. Impostos declarados não determinam automaticamente crédito aproveitável ou imposto a recolher.
- O CNPJ filtra os participantes já autorizados; não permite consultar qualquer empresa, suas filiais ou documentos referenciados sem autorização.

## Privacidade e segurança

As consultas de documentos, CNDs e notificações são somente leitura e ficam restritas aos participantes autorizados para a conexão. O plugin não oferece alteração de documentos, reprocessamento, certificados digitais, senhas ou download de XML. O arquivo de uma CND pode ser entregue pela ferramenta específica quando autorizado.

O fluxo de contato é uma ação separada: pode registrar um rascunho, anexos e uma solicitação à EF, com envio condicionado à confirmação explícita do usuário.

Descrições e anexos enviados em chamados são armazenados pela EF e podem permanecer por mais de 30 dias. A expiração de um token ou de um rascunho não exclui o chamado já registrado. A retenção segue a política de privacidade e as condições aplicáveis ao atendimento.

As solicitações são enviadas ao servidor da Eficiência Fiscal e os dados retornados ficam disponíveis ao Claude para responder ao usuário. O tratamento desses dados segue as políticas aplicáveis da EF e da conta utilizada no Claude.

- [Política de privacidade da Eficiência Fiscal](https://app.eficienciafiscal.com.br/assets/files/politica_de_privacidade.pdf)
- [Política de privacidade da Anthropic](https://www.anthropic.com/legal/privacy)

O pacote distribuído não deve conter credenciais, tokens ou documentos fiscais. Para encerrar o acesso, revogue a autorização correspondente na EF; desinstalar o plugin não deve ser usado como substituto da revogação.

## Solução de problemas

- **Participante não listado:** confira as permissões do usuário e os participantes autorizados na conexão.
- **Módulo sem licença:** quando a EF informar explicitamente essa condição, confira a disponibilidade do módulo para o participante e o escritório. Uma recusa genérica não comprova ausência de licença.
- **Ferramenta indisponível:** a funcionalidade pode não estar habilitada no servidor. Atualizar o plugin não altera as permissões nem habilita ferramentas na EF.
- **Itens ou detalhes pendentes:** informe a limitação e tente novamente posteriormente; a pendência não comprova ausência de dados no documento.
- **Limite de consultas:** aguarde o tempo indicado. Não inicie chamadas paralelas para contornar a restrição.
- **Autenticação expirada ou revogada:** inicie novamente a conexão pelo Claude e conclua o login e o consentimento na EF.

Ao solicitar suporte, informe a ferramenta, o horário com fuso e a mensagem de erro. Não envie senhas, tokens ou a URL completa do retorno OAuth.

## Conteúdo do pacote

```text
.claude-plugin/plugin.json
.mcp.json
assets/ef-logo.svg
skills/consultar-ef/SKILL.md
README.md
LICENSE
```

O manifesto identifica o plugin, `.mcp.json` configura a conexão remota e a habilidade orienta o uso das ferramentas. Este repositório de distribuição não precisa conter o código do servidor da Eficiência Fiscal.

## Contato

Desenvolvido pela **Eficiência Fiscal**. Dúvidas, suporte e relatos de problemas: [software@eficienciafiscal.com.br](mailto:software@eficienciafiscal.com.br).

## Licença

Este plugin utiliza uma [licença proprietária](LICENSE). É permitido instalar e usar o plugin para acessar a Eficiência Fiscal pelo Claude, conforme suas permissões. A redistribuição por terceiros depende de autorização escrita da EF; a distribuição pela Anthropic e as operações de hospedagem no GitHub têm as permissões específicas descritas na licença. O repositório público não torna o plugin software de código aberto nem concede acesso ao serviço ou aos dados da EF.
