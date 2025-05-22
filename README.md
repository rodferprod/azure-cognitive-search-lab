# Explorando um Índice de Pesquisa no Azure AI Search

Este resumo apresenta os principais pontos do laboratório que demonstra como implementar uma solução de pesquisa inteligente usando o Azure AI Search para extrair insights de avaliações de clientes. O cenário prático é baseado em uma cadeia nacional de cafeterias chamada Fourth Coffee, onde a solução visa facilitar a busca por insights sobre experiências dos clientes.

## Recursos Necessários do Azure

Para implementar esta solução de mineração de conhecimento, são necessários três recursos principais na assinatura do Azure:

- **Azure AI Search**: gerencia a indexação e as consultas de pesquisa
- **Azure AI Services**: fornece serviços de IA para enriquecer os dados da fonte com insights gerados por IA
- **Conta de Armazenamento**: armazena documentos brutos e outras coleções em contêineres de blob

É importante observar que os recursos de Azure AI Search e Azure AI Services precisam estar na mesma localização geográfica para funcionarem corretamente juntos.

## Processo de Implementação

### Criação dos Recursos no Azure

O laboratório orienta a criação de cada um dos recursos necessários no portal do Azure com configurações específicas. Para o Azure AI Search, recomenda-se o nível de preços Básico. Para o Azure AI Services, o nível Standard S0 é sugerido. A conta de armazenamento deve ter o acesso anônimo a blobs habilitado para facilitar o acesso aos dados durante o laboratório.

### Upload de Documentos

Após criar os recursos, o próximo passo é fazer upload das avaliações de clientes para o Azure Storage:

1. Criar um contêiner chamado "coffee-reviews" com nível de acesso público
2. Baixar os arquivos de avaliações de café do link fornecido: [mslearn-coffe-reviews](https://aka.ms/mslearn-coffee-reviews)
3. Fazer upload dos arquivos para o contêiner criado.

### Indexação de Documentos

O processo de indexação utiliza o assistente "Importar dados" do Azure AI Search para criar automaticamente um índice e um indexador para as fontes de dados:

1. Conectar-se ao contêiner de armazenamento Azure Blob
2. Adicionar habilidades cognitivas através do recurso Azure AI Services
3. Configurar os seguintes enriquecimentos:
   - Extração de nomes de locais
   - Extração de frases-chave
   - Detecção de sentimento
   - Geração de tags a partir de imagens
   - Geração de legendas para imagens

Durante este processo, também é configurada uma knowledge store para salvar os resultados dos enriquecimentos em projeções de imagens, documentos, páginas, frases-chave, entidades, detalhes e referências de imagens.

## Consulta ao Índice

Após a criação e execução bem-sucedida do indexador, o laboratório demonstra como usar o Search Explorer para testar consultas ao índice:

1. Realizar uma pesquisa geral usando "*" para retornar todos os documentos
2. Filtrar avaliações por localização (exemplo: "Chicago")
3. Filtrar avaliações por sentimento (exemplo: "negative")

Os resultados são classificados por pontuação de relevância, mostrando como o mecanismo de pesquisa avalia a correspondência entre os resultados e a consulta realizada.

## Knowledge Store

Um dos aspectos mais poderosos da solução é o knowledge store, que persiste os dados enriquecidos extraídos pelas habilidades de IA:

1. No contêiner "knowledge-store", são armazenados metadados para cada documento de avaliação
2. No contêiner "coffee-skillset-image-projection", são armazenadas as imagens extraídas dos documentos
3. Em tabelas do Azure Storage, são armazenadas entidades como frases-chave, permitindo vincular as tabelas como um banco de dados relacional

## Conclusão

Este laboratório demonstra as capacidades fundamentais do Azure AI Search para criar uma solução de mineração de conhecimento. O processo envolve a extração, enriquecimento e indexação de dados para permitir pesquisas inteligentes sobre o conteúdo. Essa abordagem pode ser aplicada a diversos cenários corporativos onde a extração de insights de dados não estruturados é necessária.

A solução implementada para a Fourth Coffee exemplifica como empresas podem transformar dados brutos em informações acionáveis, melhorando a compreensão das experiências dos clientes através de tecnologias de inteligência artificial e pesquisa cognitiva.
