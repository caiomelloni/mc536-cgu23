# Equipe CGU23

# Subgrupo A
* Caio Melloni dos Santos - 167974
* Udson Charles Batagini - 244899
* Guilherme Segolin Selmi - 173947

[Link para o binder](food-intake-analysis.ipynb)

### Questão 1
``` sql
SELECT FOOD_CODE, FCID_CODE, INGREDIENT_NUM, COMMODITY_WEIGHT
FROM RECIPES 
WHERE FOOD_CODE = 27111300 
AND MOD_CODE = 0
```

### Questão 2
``` sql
SELECT R.FOOD_CODE, R.FCID_CODE, D.FCID_Desc, R.INGREDIENT_NUM, R.COMMODITY_WEIGHT
FROM RECIPES R, FCID_Description D
WHERE D.FCID_Code = R.FCID_Code
AND R.FOOD_CODE = 27111300 
AND R.MOD_CODE = 0
```

### Questão 3
``` sql
SELECT DISTINCT CG.Crop_Group_Description
FROM RECIPES R, FCID_Description D, CROP_GROUP CG
WHERE D.FCID_Code = R.FCID_Code
AND R.FOOD_CODE = 27111300 
AND R.MOD_CODE = 0
AND CG.CGN = CG.CGL
AND D.CGN = CG.CGN
ORDER BY CG.Crop_Group_Description
```

### Questão 4
``` sql
SELECT D.FCID_Desc, COUNT(*)
FROM RECIPES R, FCID_Description D
WHERE R.FCID_CODE = D.FCID_CODE
GROUP BY D.FCID_Desc
ORDER BY COUNT(*) DESC
```

### Questão 5
``` sql
SELECT CG.Crop_Group_Description, CG.CGN, AVG(I.INTAKE)
FROM FCID_Description D, INTAKE I, CROP_GROUP CG
WHERE D.CGN = CG.CGN
AND CG.CGN = CG.CGL
AND I.FCID_Code = D.FCID_Code
GROUP BY CG.Crop_Group_Description
ORDER BY CG.CGN;
```
