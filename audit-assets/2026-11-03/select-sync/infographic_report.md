# Same key, different selection

![An illustrated assignee select: Bob moves into Project members with the same key, but the model says Bob while the select shows Alice.](infographic.png)

This AI-generated conceptual illustration accompanies [Vue issue #16099](https://github.com/vuejs/core/issues/16099) and [PR #16102](https://github.com/vuejs/core/pull/16102). It is a constructed example, not a screenshot or a reported production incident.

## Architecture and use case

A native select uses `v-model` for the assignee ID. Its options are grouped into Project members and Other people. Selecting Bob also adds him to the local project membership immediately, as an optimistic UI update. [App.vue](App.vue) contains the runnable example.

Bob keeps the same `key="bob"` and `value="bob"`. Moving him to a different `optgroup` parent creates a new option element. Stable keys identify children within a parent; they do not keep the old option node when it changes parents.

## Observed problem

In the published Vue 3.5.44 development bundle, Chrome 156 showed this result after selecting Bob and completing the update: the model was `bob`, but the native select displayed Alice at index 0. The selected Bob value still existed among the options.

The pending change value still matches the model, but that does not prove the browser kept the selected option after the list changed.

## Proposed solution

Before skipping synchronization after a single-select change, check whether the selected option survived the update. Preserve an intact selection; restore a matching option when the update disturbed it. The expected outcome is Bob in both the model and the visible select.

The source-code changes and current validation results are documented in the PR. The image does not claim the fix has shipped.

## Other illustrative use case and evidence limits

A local create-tag action can also replace a synthetic option (`key=create:vue`) with a real record (`key=tag:2`) while the selected value remains `vue`. These keys identify different entries, rather than randomly changing the identity of one record.

Both scenarios are constructed examples. Public-source research did not establish an independent production incident with this exact mechanism. Similar public select reports have different causes and are not presented as proof of production impact.

## Generation

- Tool: native `image_gen`, editing the preceding blue-and-gold observatory illustration.
- Prompt helper: `python scripts/pr_infographic_prompt.py --title ... --summary ... --docs ... --json`, executed directly with Python from `C:/Users/Nitro/Projects/t3code-publication`.
- Final file: `infographic.png`.
- Exact final prompt: [prompt.txt](prompt.txt).
- Visual inspection: Bob's unchanged identity, group movement, observed Bob/Alice mismatch, expected Bob/Bob result, and the evidence-limit caption are legible.
