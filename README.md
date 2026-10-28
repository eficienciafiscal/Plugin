# Eficiência Fiscal para Claude

Consulte documentos fiscais dos participantes autorizados na Eficiência Fiscal diretamente pelo Claude. O plugin reúne a conexão MCP e a habilidade `consultar-ef`, que orienta a seleção dos participantes, a consulta dos documentos e a interpretação dos dados disponíveis.

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
| Consumo | Uso e plano do acesso selecionado. |

A disponibilidade depende das ferramentas habilitadas no servidor, das permissões da conexão e dos dados existentes. Instalar o plugin não habilita novos acessos nem garante que todos os campos estejam preenchidos.

O MCP entrega dados para o Claude analisar. Cálculos, comparações e sínteses são feitos pelo assistente a partir dos resultados, respeitando as limitações informadas.

## Pré-requisitos

- Conta ativa na Eficiência Fiscal, com MCP habilitado para o escritório.
- Usuário com permissão de consulta aos participantes desejados.
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

## Limites e interpretação

- As pesquisas usam períodos de até 31 dias e paginação. Períodos maiores exigem consultas separadas.
- Cada página fiscal concluída consome um crédito, inclusive quando não encontra documentos. Itens e pagamentos têm paginação própria; detalhes e consultas de tributação concluídos também consomem um crédito. A medição de créditos não implica, por si só, cobrança financeira.
- As consultas fiscais devem ser sequenciais. Ao receber uma limitação, o assistente deve respeitar o tempo de espera informado pelo servidor.
- Dados ausentes ou pendentes não equivalem a zero. Uma resposta parcial não deve ser apresentada como resultado completo.
- Pagamentos declarados não comprovam liquidação bancária. Impostos declarados não determinam automaticamente crédito aproveitável ou imposto a recolher.
- O CNPJ filtra os participantes já autorizados; não permite consultar qualquer empresa, suas filiais ou documentos referenciados sem autorização.

## Privacidade e segurança

O acesso é somente leitura. As consultas ficam restritas aos participantes autorizados para a conexão. O plugin não oferece alteração de documentos, reprocessamento, certificados, senhas ou download de XML.

As solicitações são enviadas ao servidor da Eficiência Fiscal e os dados retornados ficam disponíveis ao Claude para responder ao usuário. O tratamento desses dados segue as políticas aplicáveis da EF e da conta utilizada no Claude.

- [Política de privacidade da Eficiência Fiscal](https://app.eficienciafiscal.com.br/assets/files/politica_de_privacidade.pdf)
- [Política de privacidade da Anthropic](https://www.anthropic.com/legal/privacy)

O pacote distribuído não deve conter credenciais, tokens ou documentos fiscais. Para encerrar o acesso, revogue a autorização correspondente na EF; desinstalar o plugin não deve ser usado como substituto da revogação.

## Solução de problemas

- **Participante não listado:** confira as permissões do usuário e os participantes autorizados na conexão.
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
```

O manifesto identifica o plugin, `.mcp.json` configura a conexão remota e a habilidade orienta o uso das ferramentas. Este repositório de distribuição não precisa conter o código do servidor da Eficiência Fiscal.

## Contato

Desenvolvido pela **Eficiência Fiscal**. Dúvidas, suporte e relatos de problemas: [software@eficienciafiscal.com.br](mailto:software@eficienciafiscal.com.br).
