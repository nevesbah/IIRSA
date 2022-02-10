# IIRSA

- [ ] Visualização geográfica dos projetos IIRSA, China e ILAT
- [ ] Visualização interativa por país
- [ ] Metodologia
- [ ] Disponibilização de entrevistas e publicações
- [ ] Disponibilização dos dados

## Possibilidades

- [ ] Criação de plataforma (poderia utilizar um subdomino do lantri, p.ex: iirsa.lantri.org)
- [ ] Integrar com MercoDocs

<<<<<<< HEAD
## Comandos Git
- git add .
- git commit -m "mensagem"
- git pull origin main
- git push origin main
=======
## Exemplo variaveis
## Pendências

{
inicio: "",
fim: "n/a",
eixo: "Capricornio",
codigo: "CAP91",
nome_projeto:
"CORREDOR FERROVIARIO BIOCE�NICO, TRAMO CHILE (ANTOFAGASTA � SOCOMPA)",
grupo: "G01",
etapa: "CONCLUIDO",
investimento_total: 501000000,
categoria: "binacional"
pais: ["CHILE","BRASIL"],
fonte_investimento: [(Tesouro Nacional, valor)],
geolocalizacao: [-24.042218,-69.349385],
info_extra: "http://iirsa.org/proyectos/detalle_proyecto.aspx?h=1317",
info_fonte: "IIRSA"
}
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
>>>>>>> e4d6e84d4a05573d151473cd5c43f656899c7b9e
