# Trabalho Prático 1

O notebook limpeza_dados.ipynb realizou a extração e formatação dos dados. Com base em arquivos .csv disponibilizados pelo TSE, foi possível obter informações dos candidatos, partidos e dos votos por município no estado do RS em 2022. 
Por meio dos arquivos candidatos_2022.csv, votacao_2022 e partidos_2022 resultantes, as tabelas foram criadas e inseridas no PostgreSQl. Além disso, arquivos shapefile do IBGE possibilitaram a criação dos municípios e microrregiões geográficos.

O script para criar o banco consistiu basicamente na criação de seis tabelas (as restrições de chave estrangeira, dentre outros aspectos, estão omitidas):

```
CREATE TABLE public.rs_municipios_2022 (
    gid integer NOT NULL,
    cd_mun character varying(7),
    nm_mun character varying(50),
    area_km2 double precision,
    geom public.geometry(MultiPolygon),
    populacao integer,
    taxa_de_alfabetizacao real,
    pib real,
    pib_per_capita real,
    renda_per_capita real,
    homicidios_por_100_mil_hab real,
    expectativa_de_vida_2010 real,
    idhm_2010 real
)

CREATE TABLE public.rs_microrregioes_2022 (
    gid integer NOT NULL,
    cd_micro character varying(5),
    nm_micro character varying(100),
    sigla_uf character varying(2),
    area_km2 double precision,
    geom public.geometry(MultiPolygon)
);

CREATE TABLE public.candidatos (
    nome character varying(100) NOT NULL,
    numero_partido integer NOT NULL,
    nome_partido character varying(100) NOT NULL,
    sigla character varying(20) NOT NULL,
    genero character varying(20),
    estado_civil character varying(50),
    escolaridade character varying(100),
    data_nascimento date,
    raca character varying(50)
);


CREATE TABLE public.partidos (
    nome character varying(100) NOT NULL,
    numero integer NOT NULL,
    sigla character varying(20) NOT NULL
);

CREATE TABLE public.votaveis (
    nome character varying(100) NOT NULL,
    tipo character varying(20) NOT NULL
);

CREATE TABLE public.votos (
    cd_mun character varying(7) NOT NULL,
    nome character varying(100) NOT NULL,
    qt_votos integer NOT NULL
);
```

![img](banco.png)
