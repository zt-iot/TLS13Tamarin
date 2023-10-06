`hyperfine --style=basic --runs 10 --output /results/log --export-markdown /results/results --prepare 'make clean' 'make proofs'`

# Original 
| Command | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `make proofs` | 21620.839 ± 348.573 | 21245.515 | 22256.664 | 1.00 |

