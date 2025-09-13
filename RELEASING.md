# Releasing the dataset

## Recreate the raw data from glottography-data

In case of upstream changes in glottography-data:
```shell
cldfbench download cldfbench_wikipedia2024officiallang.py
```

## Recreate the CLDF data

```shell
cldfbench makecldf cldfbench_wikipedia2024officiallang.py --glottolog-version v5.2
cldfbench cldfreadme cldfbench_wikipedia2024officiallang.py
cldfbench zenodo --communities glottography cldfbench_wikipedia2024officiallang.py
cldfbench readme cldfbench_wikipedia2024officiallang.py
```

## Validation

```shell
cldf validate cldf
```

```shell
cldfbench geojson.validate cldf
```

```shell
cldfbench geojson.glottolog_distance cldf --format tsv | csvformat -t | csvgrep -c Distance -r"^0\.?" -i | csvsort -c Distance | csvcut -c ID,Distance | csvformat -E | termgraph
```
