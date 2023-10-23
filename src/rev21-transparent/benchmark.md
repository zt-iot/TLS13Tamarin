`hyperfine --style=basic --runs 10 --output /results/log --export-markdown /results/results --prepare 'make clean' 'make proofs'`

# Original 
| Setting | Mean [s] | Min [s] | Max [s] |
|:---|---:|---:|---:|
| Tamarin 1.6.1, original TLS             | 21620.839 ± 348.573 | 21245.515 | 22256.664 |
| Tamarin 1.7.1 Transparent, original TLS | 24973.333 ± 170.076 | 24713.243 | 25207.903 |
| Tamarin 1.7.1, original TLS             | 24811.568 ± 165.262 | 24509.075 | 25085.664 |
| Tamarin 1.7.1 Transparent, modified TLS |   134.394 ± 1.045   |   133.039 |   136.376 |
