---
title: checkout
sidebar_label: checkout
id: version-1.0.x-checkout
original_id: checkout
---

Checkout a branch

| param                      | type [= default]          | description                                                                                                                                        |
| -------------------------- | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| [**fs**](./fs)             | FsClient                  | a file system implementation                                                                                                                       |
| [onProgress](./onProgress) | ProgressCallback          | optional progress event callback                                                                                                                   |
| **dir**                    | string                    | The [working tree](dir-vs-gitdir.md) directory path                                                                                                |
| **gitdir**                 | string = join(dir,'.git') | The [git directory](dir-vs-gitdir.md) path                                                                                                         |
| ref                        | string = 'HEAD'           | Source to checkout files from                                                                                                                      |
| filepaths                  | Array\<string\>           | Limit the checkout to the given files and directories                                                                                              |
| remote                     | string = 'origin'         | Which remote repository to use                                                                                                                     |
| noCheckout                 | boolean = false           | If true, will update HEAD but won't update the working directory                                                                                   |
| noUpdateHead               | boolean                   | If true, will update the working directory but won't update HEAD. Defaults to `false` when `ref` is provided, and `true` if `ref` is not provided. |
| dryRun                     | boolean = false           | If true, simulates a checkout so you can test whether it would succeed.                                                                            |
| force                      | boolean = false           | If true, conflicts will be ignored and files will be overwritten regardless of local changes.                                                      |
| return                     | Promise\<void\>           | Resolves successfully when filesystem operations are complete                                                                                      |

If the branch already exists it will check out that branch. Otherwise, it will create a new remote tracking branch set to track the remote branch of that name.

Example Code:

```js live
// switch to the master branch
await git.checkout({
  fs,
  dir: '/tutorial',
  ref: 'master'
})
console.log('done')
```

```js live
// restore the 'docs' and 'src/docs' folders to the way they were, overwriting any changes
await git.checkout({
  fs,
  dir: '/tutorial',
  force: true,
  filepaths: ['docs', 'src/docs']
})
console.log('done')
```

```js live
// restore the 'docs' and 'src/docs' folders to the way they are in the 'develop' branch, overwriting any changes
await git.checkout({
  fs,
  dir: '/tutorial',
  ref: 'develop',
  noUpdateHead: true,
  force: true,
  filepaths: ['docs', 'src/docs']
})
console.log('done')
```


---

<details>
<summary><i>Tip: If you need a clean slate, expand and run this snippet to clean up the file system.</i></summary>

```js live
window.fs = new LightningFS('fs', { wipe: true })
window.pfs = window.fs.promises
console.log('done')
```
</details>

<script>
(function rewriteEditLink() {
  const el = document.querySelector('a.edit-page-link.button');
  if (el) {
    el.href = 'https://github.com/isomorphic-git/isomorphic-git/edit/master/src/api/checkout.js';
  }
})();
</script>