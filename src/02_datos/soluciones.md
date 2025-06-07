# Soluciones
## 1
cat Pokemon.csv |awk 'NR<=10 {print $0}'
## 2
cat Pokemon.csv |awk 'END{ print NR}'
## 3
cat Pokemon.csv |awk -F, 'NF != 13  {print $0}'
## 4
cat Pokemon.csv |awk -F, ' $4 ~ /Water/ {tipo_agua++}END{print tipo_agua}'
## 5
cat Pokemon.csv |awk -F, ' $4 ~ /Water/ || $5 ~ /Water/ {tipo_agua++}END{print tipo_agua}'
## 6
cat Pokemon.csv |awk -F, ' $2 ~ /[1-9]/ {print $0}'
## 7
cat Pokemon.csv |awk -F, ' $7 < 0 || $7 > 100'|wc -l
## 8
cat Pokemon.csv |awk -F, ' $9 > $8 '
## 9
cat Pokemon.csv |awk -F, '{special=$10+$11; normal=$9+$8; if(special < normal )print $2, special, normal }'
## 10
cat Pokemon.csv |awk -F, '{nombres[$2]=1}END{for( i in nombres){print i}}'
## 11
cat Pokemon.csv |awk -F, '{nombres[$2]++}END{for( i in nombres){print i, nombres[i]}}'
## 12
cat Pokemon.csv |awk -F, '{nombres[$2]++}END{for( i in nombres){print i, nombres[i]}}'
## 13
cat Pokemon.csv |awk -F, '{linea[NR]=$0}END{i=NR; while(i>NR-10 ){print i,linea[i]; i--}}'
