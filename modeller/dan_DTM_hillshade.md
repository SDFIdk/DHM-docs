# Dan DTM Hillshade

Efter DTM og DSM er ajour i geodatabanken, kan der dannes hillshades herfra. Dette gøres ved at benytte Geodatabankens oracledatabase til at udvælge de relevante tiles. Første step er at danne en sqlite fil med de relevante tiles. 

Hvis alle aktive tiles (hele landet) ønskes: 

```
ogr2ogr -f SQLite samletdk_dtm.sqlite "OCI:<USERNAME>/<PASSWORD>@<ORACONNECTION>" -sql "select STI as path, FILNAVN as tile_name, mrow as row, mcol as col, GEOMETRI from DTM where REGISTRERINGTIL is NULL" -dialect SQLITE -nln coverage
```

Hvis alle nye, aktive tiles indenfor f.eks. de sidste 20 dage ønskes: 

```
ogr2ogr -f SQLite newest.sqlite "OCI:<USERNAME>/<PASSWORD>@<ORACONNECTION>" -sql "select STI as path, FILNAVN as tile_name, mrow as row, mcol as col, GEOMETRI from DTM where REGISTRERINGTIL IS NULL and REGISTRERINGFRA > date('now', '-20 day')" -dialect SQLITE -nln coverage
```

Udtrækket kan selvfølgelig også dannes ud fra en attribut, f.eks. AENDRINGSSTOERRELSE: 

```
ogr2ogr -f SQLite recalc.sqlite "OCI:<USERNAME>/<PASSWORD>@<ORACONNECTION>" -sql "select STI as path, FILNAVN as tile_name, mrow as row, mcol as col, GEOMETRI from DTM where REGISTRERINGTIL IS NULL and AENDRINGSSTOERRELSE > 0" -dialect SQLITE -nln coverage
```

Herefter køres qc_wrap.py: 

```
python qc_wrap.py -testname hillshade -mp 4 -tiles DTMdk.sqlite -targs "h:/hsdtm -tiledb DTMdk.sqlite"
```







