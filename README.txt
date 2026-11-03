# Laser Training

Simulador de treinamento para operadores industriais, em formato de jogo web point-and-click, no estilo dos jogos Papa Louie: cada estação do posto de trabalho é uma tela.

Projeto Integrador para a Indústria Santa Clara. O jogo reproduz as etapas de uma operação real com base nas Instruções de Trabalho (ITs), avalia o operador pelo desempenho e registra a evolução.

**Versão 1.0** (protótipo)

## Máquinas

- Laser industrial: corte de flange
- Prensa industrial: conformação de suporte

## Como funciona

O operador entra com a matrícula, escolhe a máquina e passa por 5 estações. A IT da peça do pedido fica sempre visível ao lado da tela.

| Estação | Laser | Prensa |
|---|---|---|
| 1. Segurança | EPIs, inspeção da área, bloqueio de energia (LOTO) | idem |
| 2. Máquina | chapa, bico e gás | chapa, matriz e lubrificante |
| 3. Sequência | programa de corte | montagem da matriz e partida |
| 4. Ajuste | pressão do gás, foco, altura do bico | força, altura de fechamento, golpes por minuto |
| 5. Execução | corte (animação automática) | prensagem (animação automática) |

- As estações 2 a 5 só abrem depois da Segurança.
- Cada erro gera feedback imediato, sem revelar a resposta.
- Nota de 0 a 100: 60% taxa de acertos, 20% aderência à sequência da IT e 20% tempo, menos descontos por erro (maiores nos erros de segurança). Aprovado com 70 ou mais.
- Cada sessão registra nota, tempo e erros por estação (segurança, máquina, código e ajuste).
- Sessões de cerca de 5 a 15 minutos, com interface visual e controles simples.

## Como rodar

Abra o `treinamento_laser.html` no navegador. Não precisa instalar nada.

Nesse modo (teste), qualquer matrícula é aceita e os resultados ficam guardados só no navegador.

## Banco de dados (opcional)

O `backend_banco.js` é um servidor Node com SQLite que valida a matrícula e grava os resultados.

```bash
npm init -y
npm i express better-sqlite3 cors
node backend_banco.js
```

O servidor sobe em `http://localhost:3000` e também serve o `treinamento_laser.html`.

Para ligar o jogo ao banco, no `treinamento_laser.html`:

1. Comente as duas funções marcadas como `MODO TESTE`.
2. Descomente o bloco `BANCO REAL` e ajuste `API_URL`.

Antes disso, cadastre os operadores na tabela `operadores` (há um exemplo comentado no `backend_banco.js`). Só matrículas cadastradas entram no jogo.

Tabelas: `operadores` e `sessoes_treino`.

## Arquivos

| Arquivo | Descrição |
|---|---|
| `treinamento_laser.html` | O jogo (arquivo único) |
| `backend_banco.js` | Servidor com banco SQLite |
| `gabarito.txt` | Respostas de todas as estações |

## Limitações da versão 1.0

- O conteúdo (peças, parâmetros, EPIs e procedimentos) é fictício. Precisa ser trocado pelos dados reais das ITs da empresa.
- Não há painel de acompanhamento para o líder. Os dados ficam no banco quando a integração está ativa.
- Cada máquina tem um único treinamento.
