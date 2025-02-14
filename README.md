# Redis Leaderboard Challenge

## Sobre o Projeto
Este é um desafio de backend focado na implementação de um sistema de ranking (leaderboard) utilizando Redis. O objetivo é criar uma API que permita gerenciar pontuações de jogadores e exibir um ranking atualizado.

O desafio é perfeito para:
- Praticar desenvolvimento de APIs
- Aprender sobre Redis e seus casos de uso
- Experimentar com diferentes padrões de comunicação (REST/WebSocket)
- Desenvolver código limpo e organizado seguindo boas práticas

Não há restrições quanto à linguagem de programação - escolha a que você se sente mais confortável!

## Ferramentas Utilizadas

### Redis
Redis é um armazenamento de estrutura de dados em memória, usado como banco de dados, cache, message broker e queue. Para este desafio, utilizaremos especialmente os Sorted Sets do Redis, que são perfeitos para implementação de leaderboards pois:
- Mantêm os elementos ordenados por score
- Oferecem operações atômicas de atualização
- Permitem recuperação rápida do ranking
- Escalam bem para grandes conjuntos de dados

### RedisInsight
RedisInsight é uma ferramenta de interface gráfica para Redis que permite:
- Visualizar e interagir com os dados armazenados
- Monitorar o desempenho do Redis
- Executar comandos e consultas
- Depurar sua aplicação

Durante o desenvolvimento, você poderá usar o RedisInsight para verificar se os dados estão sendo corretamente armazenados e manipulados.

### Docker e Docker Compose
Para facilitar o desenvolvimento e garantir um ambiente consistente, o projeto utiliza Docker e Docker Compose para orquestrar os containers necessários. A infraestrutura inclui:
- Um container Redis para armazenamento dos dados
- Um container RedisInsight para visualização e gerenciamento
- Volumes persistentes para manter os dados entre reinicializações
- Healthchecks para garantir que os serviços estão funcionando corretamente

## Desafio Técnico

### Descrição
O desafio consiste em desenvolver uma API para um sistema de ranking (leaderboard) onde:

1. Cada jogador é identificado por um nome único
2. Cada jogador possui uma pontuação que pode ser atualizada
3. O ranking deve estar sempre ordenado pela pontuação (maior para menor)
4. As operações devem ser eficientes utilizando as capacidades do Redis

A implementação deve utilizar Redis Sorted Sets para gerenciar o ranking, aproveitando suas características de ordenação automática e performance.

## Requisitos da API

### Obrigatórios
- [ ] Implementar endpoint POST /score para adicionar ou atualizar pontuação
  - Deve aceitar nome do jogador e pontuação
  - Deve retornar a posição atual do jogador no ranking
  - Deve atualizar a pontuação do jogador

- [ ] Implementar endpoint GET /leaderboard para consultar o ranking
  - Deve retornar lista ordenada dos jogadores
  - Deve incluir posição, nome e pontuação de cada jogador
  - Opcional: Implementar paginação

- [ ] Utilizar Redis Sorted Sets apropriadamente
  - Usar comandos apropriados para inserção e atualização (ZADD)
  - Usar comandos eficientes para recuperação do ranking (ZREVRANGE)
  - Implementar tratamento de erros adequado

### Opcionais
- [ ] Implementar endpoints adicionais
  - GET /scores/{player} para consultar posição específica
  - GET /leaderboard/top/{n} para consultar top N jogadores
  - DELETE /scores/{player} para remover jogador

- [ ] Implementar WebSocket para atualizações em tempo real
  - Enviar o leaderboard completo atualizado quando houver mudança de pontuação
  - Manter conexão eficiente e gerenciar reconexões
  - Implementar protocolo de heartbeat para manter conexões ativas

- [ ] SUPER BONUS: Otimização das atualizações em tempo real
  - Implementar paginação nas atualizações via WebSocket
  - Enviar atualizações apenas quando o top N (ex: top 20) for afetado
  - Permitir que clientes escolham o tamanho da página que desejam observar
  - Incluir metadados como página atual e indicador de mudança no top N

## Como Executar

### Pré-requisitos
Para executar este projeto, você precisará ter instalado:
- Docker
- Docker Compose
- Git

Todos os outros serviços (Redis e RedisInsight) serão executados em containers.

### Rodando o Projeto
1. Clone este repositório:
```bash
git clone https://github.com/defermenot/live-leaderboard.git
cd live-leaderboard
```

2. Inicie os serviços com Docker Compose:
```bash
docker-compose up -d
```

3. Verifique se os serviços estão rodando:
```bash
docker-compose ps
```

Os serviços estarão disponíveis em:
- Redis: localhost:6379
- RedisInsight: http://localhost:5540

Para parar os serviços:
```bash
docker-compose down
```

Para visualizar os logs:
```bash
docker-compose logs -f
```

## Testando a API

### Usando Postman/Insomnia
### Usando Postman
1. Importe a coleção de exemplo (disponível em `docs/postman-collection.json`)
2. Configure a variável de ambiente `base_url` para sua API
3. Use os endpoints pré-configurados para testar
4. Para WebSocket, utilize a funcionalidade WebSocket do Postman

### Usando Insomnia
1. Importe o workspace de exemplo (disponível em `docs/insomnia-workspace.json`)
2. Configure a variável de ambiente `base_url`
3. Use os endpoints pré-configurados para testar
4. Para WebSocket, utilize a aba WebSocket do Insomnia

## Como Submeter sua Solução

### Fork
1. Faça um fork do repositório através do botão "Fork" no GitHub

2. Clone seu fork:
```bash
git clone https://github.com/seu-usuario/live-leaderboard.git
cd live-leaderboard
```

3. Crie uma branch para sua implementação:
```bash
git checkout -b feature/minha-implementacao
```

4. Implemente sua solução e faça commits:
```bash
git add .
git commit -m "Implementação do leaderboard com Redis"
```

5. Envie para seu fork:
```bash
git push origin feature/minha-implementacao
```

6. Abra um Pull Request:
   - Vá para a página do repositório original
   - Clique em "Pull Requests"
   - Clique em "New Pull Request"
   - Selecione sua branch
   - Preencha as informações solicitadas
   - Submeta o PR

Dicas para o Pull Request:
- Descreva sua implementação
- Mencione quais funcionalidades opcionais foram implementadas
- Liste as tecnologias/frameworks utilizados
- Inclua instruções específicas de como rodar seu projeto, se necessário

## Links Úteis

### Redis Documentation
- [Redis Sorted Sets](https://redis.io/docs/data-types/sorted-sets/)
- [Redis Leaderboard Pattern](https://redis.com/solutions/use-cases/leaderboards/)

### API Development
- [REST API Best Practices](https://restfulapi.net/)
- [WebSocket Best Practices](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)

### Development Tools
- [Postman](https://www.postman.com/)
- [Insomnia](https://insomnia.rest/)
- [RedisInsight Documentation](https://redis.com/redis-enterprise/redis-insight/)
