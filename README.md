# IIRSA

- [ ] Visualização geográfica dos projetos IIRSA, China e ILAT
- [ ] Visualização interativa por país
- [ ] Metodologia
- [ ] Disponibilização de entrevistas e publicações
- [ ] Disponibilização dos dados

## Possibilidades

- [ ] Criação de plataforma (poderia utilizar um subdomino do lantri, p.ex: iirsa.lantri.org)
- [ ] Integrar com MercoDocs

## Pendências

- [ ] Problemas de enconde (acentuação no json)
- [ ] Paises duplicados
- [ ] Geolocalização (dict)



|Variáveis| Tipo| Exemplo |
| ------- |-----|-----|
|geolocalização|`dict`| {x: geo01, y:geo02}
|paises|`list`||
|fonte de investimento| `list/tuple`||


```
[(tesouro,10), [bndes,20]]

[{tesouro:10},{bndes:20}]

fonte_investimento: {fonte:[tesouro, bid], valor: [10,20]}

```
