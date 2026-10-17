---
name: pesquisa-produtos
description: "Pesquisa produtos em sites de vendas usando navegação estruturada, busca por campo, categoria e paginação limitada; extrai dados verificáveis e gera um resumo em Markdown. Use para pesquisas de livros e produtos."
argument-hint: "Informe o site, os termos de busca, filtros opcionais e a quantidade de resultados desejada."
user-invocable: true
---

# Pesquisa de Produtos

## Objetivo

Pesquisar produtos em um site de vendas e gerar um resumo estruturado em Markdown, utilizando apenas dados confirmados nas páginas do site.

## Entradas

Solicite ou identifique:

- **Site:** URL inicial do site de vendas.
- **Termos de busca:** um ou mais nomes, títulos ou descrições de produtos.
- **Filtros (opcionais):** categoria, faixa de preço, avaliação, disponibilidade, marca, idioma ou outros filtros disponíveis no site.
- **Quantidade de resultados:** limite de resultados a registrar para cada termo de busca.

Se a quantidade de resultados não for informada, peça esclarecimento antes de coletar ou use o limite explicitamente definido pela solicitação. Não ultrapasse o limite solicitado.

## Passo a passo

1. Acesse a URL inicial usando o navegador ou a ferramenta de navegação disponível.
2. Verifique se o site possui um campo de busca funcional.
3. **Busca direta:** se houver campo de busca, pesquise cada termo individualmente e aplique os filtros informados.
4. **Busca por categoria:** se não houver campo de busca, não percorra o catálogo inteiro. Para cada termo, identifique a categoria mais provável no menu ou na estrutura do site e pesquise somente dentro dela.
5. **Paginação limitada:** se o item não for encontrado na categoria provável, retorne ao catálogo principal e percorra no máximo 5 páginas. Pare imediatamente ao alcançar esse limite.
6. Ao localizar um resultado, abra a página de detalhes do produto.
7. Extraia somente os campos disponíveis e verificáveis, conforme o site:
   - título;
   - preço;
   - disponibilidade ou quantidade em estoque;
   - avaliação;
   - categoria;
   - URL da página de detalhes, quando útil;
   - descrição ou resumo.
8. Para o primeiro resultado encontrado de cada termo, leia a descrição completa disponível e escreva um resumo de 2 a 3 linhas no idioma solicitado. Se nenhum idioma for solicitado, use português.
9. Pare a coleta de cada termo quando atingir a quantidade de resultados solicitada.
10. Salve o resultado no arquivo Markdown solicitado pelo usuário. Se o caminho não for informado, use `resultado-busca.md` na raiz do projeto.
11. Valide o arquivo final e informe quais categorias foram visitadas e quantas páginas foram percorridas para termos não encontrados.

## Regras

- Não invente resultados, preços, estoque, avaliações, categorias, descrições ou resumos.
- Se um termo não for encontrado, registre **Não encontrado** e informe detalhadamente onde procurou, incluindo categorias visitadas e quantidade de páginas percorridas.
- Não registre dados pessoais de vendedores, compradores ou outros usuários.
- Respeite a quantidade máxima de resultados solicitada para cada termo.
- Respeite o limite máximo de 5 páginas na paginação do catálogo principal.
- Não percorra o catálogo inteiro quando houver uma categoria provável disponível.
- Não trate um produto semelhante como correspondência exata sem indicar claramente a diferença.
- Preserve a grafia e o título exibidos na página de detalhes.
- Não substitua dados ausentes por valores estimados; registre `Não informado` quando apropriado.
- Se houver falha de acesso, carregamento ou navegação, registre a falha e não apresente dados não verificados como resultado.

## Formato do arquivo de saída

Use a seguinte estrutura:

```markdown
# Resultado da busca em [nome do site]

## Estratégia executada

1. **Busca direta:** [informar se existia e foi usada; ou informar que não existia].
2. **Busca por categoria:** [categorias visitadas e termos pesquisados].
3. **Paginação limitada:** [páginas percorridas, no máximo 5, ou informar que não foi necessária].

## Resultados

### [Termo ou produto]

**Encontrado** ou **Não encontrado**

- **Título:** [título confirmado]
- **Preço:** [preço]
- **Disponibilidade:** [estoque ou status]
- **Avaliação:** [avaliação]
- **Categoria:** [categoria]
- **URL:** [URL da página de detalhes]
- **Resumo:** [2 a 3 linhas em português para o primeiro resultado do termo]

## Observações

[Limitações, falhas de acesso, categorias visitadas e páginas percorridas, quando aplicável.]
```

Quando um termo não for encontrado, substitua os campos de produto por um relato da busca:

```markdown
### [Termo]

**Não encontrado**

- **Categorias visitadas:** [categorias]
- **Páginas percorridas:** [quantidade e páginas]
- **Motivo:** [explicação verificável]
```
