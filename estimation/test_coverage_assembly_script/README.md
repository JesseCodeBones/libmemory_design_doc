# Estimation for new Assembly Script Test Coverage Optimization

## current status  

  |File               | % Stmts | % Branch | % Funcs | % Lines |
  |-------------------|---------|----------|---------|---------|
  |ast.ts             |   96.11 |     93.3 |   92.89 |   96.11 |
  |bindings.ts        |     100 |      100 |     100 |     100 | 
  |builtins.ts        |   76.93 |    71.76 |   75.42 |   76.93 |
  |common.ts          |     100 |      100 |     100 |     100 | 
  |compiler.ts        |   86.15 |     81.8 |   93.02 |   86.15 |
  |diagnostics.ts     |   92.71 |    95.54 |      90 |   92.71 |
  |flow.ts            |   97.11 |       90 |   66.66 |   97.11 |
  |index-js.ts        |   94.73 |       40 |    0.86 |   94.73 |
  |index-wasm.ts      |     100 |      100 |     100 |     100 |
  |index.ts           |     100 |      100 |     100 |     100 |
  |module.ts          |   82.98 |    82.59 |   57.47 |   82.98 |
  |parser.ts          |   91.06 |    82.38 |     100 |   91.06 |
  |program.ts         |   91.33 |    84.64 |   90.96 |   91.33 |
  |resolver.ts        |   87.84 |    74.68 |      85 |   87.84 |
  |tokenizer.ts       |   89.94 |    84.39 |   79.29 |   89.94 |
  |types.ts           |   96.39 |    86.13 |   94.28 |   96.39 |
  |util.ts            |     100 |      100 |     100 |     100 |

## TODO files
|File        | covered lines / total lines|
|------------|----------------------------|
|builtins.ts | 8012/10414|
|compiler.ts | 9155/10626|
|module.ts   | 2731/3291 |
|resolver.ts | 3072/3497 |
|tokenizer.ts| 1584/1761 |

## estimation
according to above information, we missed **5,035 lines**.
additional, we fixed `parser.ts` test coverage around 450 lines, and it cost us 6 days.  
we estimate we can fix 70% of the missed lines, that is 3500 lines.  
so we estimate the working day is (3500 / 450) * 6 = **46 days**  
