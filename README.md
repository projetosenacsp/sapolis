# SApólis EdTech

Plataforma de preparação para o ENEM em que cada conteúdo parte de um lugar de São Paulo. A **Lumiri** guia o estudante por rotas de estudo, minijogos, missões pela cidade e pelo **SApólis Vision** (câmera e mapa).

> **Prévia beta.** Algumas funções são demonstrativas ou estão em desenvolvimento (veja [Estado das funcionalidades](#estado-das-funcionalidades)).

**Prévia online:** _será preenchido com o endereço gerado pela Vercel após o primeiro deploy._

## Funcionalidades

- **Primeiro acesso guiado:** apresentação (7 telas) → preferências → tutorial da Lumiri → plataforma. O progresso do onboarding é salvo e retomado.
- **Biblioteca ENEM:** 8 rotas (Matemática, Redação, Biologia, Física, Química, Geografia, Português e História) com lição em 7 etapas, questões de treino e minijogos.
- **Missões pela Cidade:** Quebra-cabeça, Conecte os Conceitos, Linha do Tempo, Investigação ENEM e Desafio Relâmpago.
- **Monte a Fórmula:** matemática gamificada com validação por equivalência.
- **Laboratório de Redação** e **Conexões Invisíveis** (percursos entre disciplinas).
- **SApólis Vision:** descoberta de lugares pela câmera (modo demonstrativo) e pelo mapa interativo.
- **Trilhas para focar:** sons gerados no próprio navegador.
- **XP, níveis, ofensiva diária e conquistas**, com histórico na ilha dinâmica.
- Modos de aparência: Roxo original, Preto e branco e Branco.

## Estado das funcionalidades

| Funcionalidade | Estado |
|---|---|
| Rotas, lições, questões e minijogos | Funcionando |
| XP, conquistas e progresso | Funcionando (salvos no navegador do estudante) |
| Mapa de São Paulo | Funcionando (tiles do OpenStreetMap) |
| Câmera do SApólis Vision | Funciona em HTTPS, com permissão do navegador; a foto é processada só no aparelho e descartada |
| Reconhecimento de lugares por foto | **Não conectado.** Hoje o estudante escolhe o lugar manualmente ou usa os exemplos demonstrativos |
| Ranking da Comunidade | **Demonstrativo** (não há outros usuários reais) |
| ENEM Premium | **Demonstrativo** (sem cobrança nem assinatura) |
| Lumiri Running, Cartas do Conhecimento, Trilhas narradas | **Em desenvolvimento** (aparecem só como arte ilustrativa na apresentação) |

## Tecnologias

HTML, CSS e JavaScript nativos em um único arquivo (`index.html`), sem etapa de build.

- [Tailwind CSS](https://tailwindcss.com/) via CDN
- [Leaflet](https://leafletjs.com/) 1.9.4 via cdnjs (mapa)
- Fonte Inter e Caveat (Google Fonts)
- `localStorage` para progresso, preferências e tema (nenhum dado sai do aparelho)

## Estrutura

```
index.html      aplicativo
capas/          capas das disciplinas, dos jogos e ícones
*.png / *.jpg   artes da Lumiri e da apresentação
fontes/         artes originais em alta resolução e materiais de apoio (não vão para o site)
vercel.json     cabeçalhos de segurança e permissões
```

## Executar localmente

A câmera e a localização só funcionam em contexto seguro (HTTPS ou `localhost`), por isso não abra o arquivo direto pelo explorador. Na pasta do projeto:

```bash
python -m http.server 8080
```

e acesse `http://localhost:8080`.

Para refazer o primeiro acesso sem apagar o progresso, abra `http://localhost:8080/?onboarding=reset` ou use **Perfil › Reiniciar só o onboarding (teste)**.

## Publicar (GitHub + Vercel)

1. No GitHub, crie o repositório `sapolis-edtech` e envie o código (`git push -u origin main`).
2. Na [Vercel](https://vercel.com/new), importe o repositório. Deixe **Framework Preset: Other**, sem comando de build e com o diretório de saída na raiz (o `vercel.json` já define isso).
3. Clique em **Deploy**. O endereço `https://<projeto>.vercel.app` passa a ser a prévia pública.

### Atualizações

| Ação no GitHub | Resultado na Vercel |
|---|---|
| `git push` na branch `main` | Novo deploy de **produção** |
| `git push` em qualquer outra branch ou Pull Request | Deploy de **prévia**, com endereço próprio, para testar sem afetar a produção |

Fluxo recomendado: trabalhe em uma branch (`git checkout -b minha-mudanca`), teste o endereço de prévia e só então faça o merge em `main`.

## Privacidade

- Nenhum dado de estudante é enviado a servidores: tudo fica no `localStorage` do navegador.
- Fotos tiradas ou escolhidas no SApólis Vision não são armazenadas nem enviadas; são descartadas após o uso.
- A localização é opcional, pedida só ao toque e nunca salva.
- Não há chaves de API, tokens ou senhas no código.
