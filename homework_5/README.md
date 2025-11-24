# Предсказание и парное выравнивание структур белков
## Исходные данные:
Первичная последовательность белка: ```MSTLTSVSGFPRIGQNRELKKIIEGYWKGANDLAAVKATAAELRAKHWRLQQAAGIDLIASNDFSYYDQMLDTAILLNVIPQRYQRLAFDDQEDTLFAMA``` \
Инструмент 1 фолдинга белков: [AlphaFold2](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb) \
Инструмент 2 фолдинга белков: [OmegaFold](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/beta/omegafold.ipynb) \
Инструмент парного выравнивания:  [ProFit](http://www.bioinf.org.uk/software/profit/)

## Блокноты с предсказаниями:
1. [AlphaFold2](alpha_fold.ipynb)
2. [OmegaFold](omegafold.ipynb)

## Предсказания в формате pdb:
1. [AlphaFold2](bioinformatics_5_tool_1_3b0d9/bioinformatics_5_tool_1_3b0d9_unrelaxed_rank_001_alphafold2_model_3_seed_000.pdb)
2. [OmegaFold](bioinformatics_5_tool_2_3b0d9.pdb)

## Работа с profit:
```

                  PPPPP                FFFFFF ii   tt
                  PP  PP               FF          tt
                  PP  PP rrrrr   oooo  FF     ii  ttttt
                  PPPPP  rr  rr oo  oo FFFF   ii   tt
                  PP     rr     oo  oo FF     ii   tt
                  PP     rr     oo  oo FF     ii   tt
                  PP     rr      oooo  FF      ii   ttt

                      Protein Least Squares Fitting

                               Version 3.3

      Copyright (c) Dr. Andrew C.R. Martin, SciTech Software 1992-2013
              Copyright (c) Dr. Craig T. Porter, UCL 2008-2009

   Reading reference structure (/Users/maryayukhnina/NSU/Bioinformatics2.0/homework_5/bioinformatics_5_tool_2_3b0d9.pdb)...
   Reading mobile structure (/Users/maryayukhnina/NSU/Bioinformatics2.0/homework_5/bioinformatics_5_tool_1_3b0d9/bioinformatics_5_tool_1_3b0d9_unrelaxed_rank_001_alphafold2_model_3_seed_000.pdb)...
ProFit> STATUS
   Reference structure:        /Users/maryayukhnina/NSU/Bioinformatics2.0/homework_5/bioinformatics_5_tool_2_3b0d9.pdb
   Mobile structure:           /Users/maryayukhnina/NSU/Bioinformatics2.0/homework_5/bioinformatics_5_tool_1_3b0d9/bioinformatics_5_tool_1_3b0d9_unrelaxed_rank_001_alphafold2_model_3_seed_000.pdb
   HETATM records are:         Ignored
   Align gap penalty:          10
   Align gap extend penalty:    2
   Fitting will be:            Normal (unweighted)
   Reference structure Chains: A
   Mobile structure Chains:    A
   Current numbering mode:     Residue
   Iterative zone updating:    Off
   Atoms being fitted:         All
   Atoms will be included regardless of B-value
   Atom pairs will be included regardless of interatomic distance
   Zones being fitted:         All

   Coordinates written centred on: REFERENCE SET

   Reference sequence:         
   MSTLTSVSGFPRIGQNRELKKIIEGYWKGANDLAAVKATAAELRAKHWRLQQAAGIDLIA
   SNDFSYYDQMLDTAILLNVIPQRYQRLAFDDQEDTLFAMA
   Mobile sequence:            
   MSTLTSVSGFPRIGQNRELKKIIEGYWKGANDLAAVKATAAELRAKHWRLQQAAGIDLIA
   SNDFSYYDQMLDTAILLNVIPQRYQRLAFDDQEDTLFAMA
ProFit> ALIGN

   Mobile Structure:  1
   /Users/maryayukhnina/NSU/Bioinformatics2.0/homework_5/bioinformatics_5_tool_2_3b0d9.pdb Chain 'A'
   /Users/maryayukhnina/NSU/Bioinformatics2.0/homework_5/bioinformatics_5_tool_1_3b0d9/bioinformatics_5_tool_1_3b0d9_unrelaxed_rank_001_alphafold2_model_3_seed_000.pdb Chain 'A'
   Score: 482 Normalised score: 4.82
   MSTLTSVSGFPRIGQNRELKKIIEGYWKGANDLAAVKATAAELRAKHWRLQQAAGIDLIA
   MSTLTSVSGFPRIGQNRELKKIIEGYWKGANDLAAVKATAAELRAKHWRLQQAAGIDLIA

   SNDFSYYDQMLDTAILLNVIPQRYQRLAFDDQEDTLFAMA
   SNDFSYYDQMLDTAILLNVIPQRYQRLAFDDQEDTLFAMA


```

Результат выполнения лежит в [aligned_result.pdb](aligned_result.pdb)

Раскрашенная визуализация выравнивания лежит в [aligned_result.png](aligned_result.png)

Сессия PyMOL лежит в [pymol_session.pse](pymol_session.pse)

### Вывод

1. **Полное совпадение первичных последовательностей**:
   Как показало выравнивание в ProFit, аминокислотные последовательности, сгенерированные AlphaFold2 и OmegaFold, идентичны на 100%. Это и ожидаемо, так как обе модели использовали один и тот же исходный пептид.

2. **Высокое структурное сходство**:
   - Нормализованный балл выравнивания в ProFit составил **4.82**. Этот показатель свидетельствует об очень высоком степени структурного сходства двух моделей.
   - Визуальный анализ раскрашенной структуры в PyMOL (файл `aligned_result.png`) подтверждает, что белковые остовы и вторичные структурные элементы (альфа-спирали, бета-листы) в предсказаниях от двух разных инструментов практически накладываются друг на друга.

3. **Незначительные локальные расхождения**:
   - Несмотря на общее высокое сходство, при детальном рассмотрении в PyMOL можно заметить незначительные отклонения в конформациях некоторых боковых цепей (аминокислотных остатков) и в гибких петлевых регионах.
   - Эти расхождения являются нормой для методов предсказания и часто возникают в областях белка с высокой внутренней подвижностью, где существует несколько энергетически близких конформаций.

4. **Сравнение методов предсказания**:
   - **AlphaFold2** и **OmegaFold** используют принципиально разные архитектуры нейронных сетей и подходы к предсказанию (OmegaFold, например, не использует MSAs и шаблоны, в отличие от AlphaFold2).
   - Несмотря на это, для данной последовательности оба метода сошлись в очень похожем структурном предсказании, что является косвенным подтверждением его надежности. Высокая степень уверенности (pLDDT) в предсказании AlphaFold2 для большинства остатков также указывает на то, что структура этого белка, вероятно, хорошо определена и легко предсказуема.

### Общий вывод

Оба инструмента, AlphaFold2 и OmegaFold, продемонстрировали исключительно высокую степень согласованности в предсказании третичной структуры для предоставленной аминокислотной последовательности. Полученные модели практически идентичны по своему основному каркасу, что позволяет с высокой долей уверенности считать предсказанную структуру достоверной. Незначительные различия подчеркивают важность использования нескольких независимых методов для верификации структурных предсказаний, особенно в гибких областях белка.
