# SCP-CS solutions

Solutions of the set covering problem with conflicts on sets (SCP-CS) of Carrabs et al. (2024), from a computational
study on the benchmark instances of Carrabs et al. (2024), on Set D of Song et al. (2026), on 30 new large instances,
on three rail instances of OR-Library and on a Wi-Fi planning instance, together with the reference solutions they are
compared with. The reference of the article will be added here when it is published.

## Cost of a solution

An instance has m elements and n subsets S_1, ..., S_n with integer costs c_j. A solution is a set X of subsets that
covers every element, and its cost is

    cost = sum of c_j over j in X  +  sum over the pairs i < j in X of kappa * max(0, |S_i ∩ S_j| - k)

that is, the subset cost plus the conflict cost. Every row gives the threshold k and the overlap price kappa. On the
benchmark, Set D, large and rail instances, kappa = max(1, round(max_j c_j / |S_j|)), with ties rounded to even, as
in the code of Carrabs et al. (2024); on the Wi-Fi instances it is set explicitly.

## Files

The folder `solutions/` holds one CSV file per group of solutions, with one row per solution and the columns

- `instance`, `k`, `kappa`: the case;
- `seed`: the run (`rail.csv` also gives the `implementation`); in the files of reference solutions, `plan` names the
  solution instead;
- `cost`, `subset_cost`, `conflict_cost`: the cost of the solution and its two parts;
- `size`: the number of selected subsets;
- `subsets`: the selected subsets, numbered from 1 as in the instance files, in increasing order and separated by
  spaces.

| File | Rows | Solutions |
|---|---:|---|
| `benchmark.csv` | 1840 | the 80 instances of Carrabs et al. (2024), with k = 1 and 2 (10 runs each) and k = 3 (3 runs) |
| `set_d.csv` | 240 | the 40 instances of Set D, with k = 1, 2 and 3 (2 runs each) |
| `large.csv` | 180 | the 30 large instances, with k = 1 and 2 (3 runs each) |
| `large_grasp.csv` | 180 | the same cases, solved by the parallel GRASP of Carrabs et al. (2024) with its authors' code |
| `rail.csv` | 54 | rail507, rail516 and rail582, with k = 1, 2 and 3: 3 runs each of a CPU and of a GPU implementation |
| `rail_classical_plans.csv` | 54 | the 6 distinct optimal covers of the classical set covering model (without conflicts) of each rail instance found by HiGHS, numbered by `plan` and evaluated for each k |
| `wifi.csv` | 23 | the Wi-Fi instance `valpo_wifi` with k = 2 and kappa = 42 (5 runs), k = 1 and 4 with kappa = 42, and k = 2 with kappa = 21 and 84; and its variants `valpo_wifi_pr04` and `valpo_wifi_pr08` with k = 2 (3 runs in every other case) |
| `wifi_reference_plans.csv` | 14 | for the same cases, the best plans found by HiGHS in 600 s for the minimum-cost covering and for the linear overlap model (`plan`) |

## Instances

- Benchmark: the files `<instance>-3.txt` of `datasets/beasley` in https://github.com/lmores/or-scp-cs-src, the code
  of Carrabs et al. (2024).
- Set D: the instances of Song et al. (2026) were not available, so these runs use a reconstruction from the weighted
  set covering instances of Vasko et al. (2025), with the columns merged by threes as Song et al. (2026) describe.
- Rail: rail507, rail516 and rail582 of OR-Library (Beasley, 1990), used as they are, with the subsets numbered as
  there.
- Large and Wi-Fi: the 30 large instances (scpl11 to scpl65) and the Wi-Fi instances are new and will be published
  with the article. The Wi-Fi instances cover Valparaíso – Viña del Mar (Chile) and are built from OpenStreetMap data
  and SRTM elevation data; `valpo_wifi_pr04` and `valpo_wifi_pr08` set the ratio of the cost of a public site to the
  cost of a private site to 0.4 and 0.8, instead of 0.6.

## License

CC BY 4.0. The Wi-Fi instances are derived from OpenStreetMap data, © OpenStreetMap contributors, available under
the Open Database License (ODbL 1.0).

## References

- Beasley, J. E. (1990). OR-Library: Distributing test problems by electronic mail. Journal of the Operational
  Research Society, 41(11), 1069–1072. https://doi.org/10.1057/jors.1990.166
- Carrabs, F., Cerulli, R., Mansini, R., Moreschini, L., & Serra, D. (2024). Solving the set covering problem with
  conflicts on sets: A new parallel GRASP. Computers & Operations Research, 166, 106620.
  https://doi.org/10.1016/j.cor.2024.106620
- Song, M. S., Cadiz, P., Lu, Y., Swan, E., & Vasko, F. J. (2026). A simple hybrid approach for solving set covering
  problems with conflict constraints. Mathematics, 14(2), 342. https://doi.org/10.3390/math14020342
- Vasko, F. J., Lu, Y., Song, M. S., & Rando, D. (2025). Filling the gap in weighted set covering problem test
  instances: Implications for both researchers and practitioners. International Journal of Industrial Optimization,
  6(1), 17–27. https://doi.org/10.12928/ijio.v6i1.10836
