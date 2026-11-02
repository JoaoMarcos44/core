# Vue Core functional bug reproductions and illustrations

These materials accompany three focused Vue Core contributions. The source-code PRs keep their changes separate from these explanatory assets.


- [#16098: Reactive props destructure rewrites shadowed catch and switch bindings](compiler-scopes/infographic_report.md)
- [#16099: Select displays a different value from v-model after replacing the selected option during change](select-sync/infographic_report.md)
- [#16100: effect() mutates shared options and rejects frozen options in the ESM build](effect-options/infographic_report.md)

Each folder includes a runnable SFC Playground link, App.vue, infographic.png and the exact image-generation prompt. No P0/P1 severity claim is made; the reports describe the observed impact.
