# example-markdown-rendering-bug

A simple repro of a markdown rendering bug for local links inside a note block.

Here we demonstrate that relative links in a file only work in the main `README.md` file (which is rendered by default when we arrive at the root of the repo), when they are *outside* of a "note" block.

## Works

Test link that works: [`TestLinkedFile.md`](./TestLinkedFile.md)

The link above gets rendered to a `/repo-name/tree/branch-name/path/to/file` style link

Note: the `/tree/branch-name/` portions are *automatically* added.

## Doesn't Always Work

> Test link that doesn't always work: [`TestLinkedFile.md`](./TestLinkedFile.md)

However, the link inside the "note" block (prefixed with a `>` character), is not always rendered correctly.

There are two cases:

- The user visits the root of the repo (__the broken case__):

  For instance: <https://github.com/bpkroth/example-markdown-rendering-bug>

  In this case the link in the note block is rendered as `https://github.com/bpkroth/TestLinkedFile.md` instead.

  That is, it is missing the `/tree/branch-name/` portion, which makes some sense given that we're at the root of the repo, but it's still a bug since it's not consistent with the other link above, and it's not a valid link.

- The user visits the file under the source tree.

  For instance: <https://github.com/bpkroth/example-markdown-rendering-bug/tree/main/README.md>

  This can happen for instance after following the [`TestLinkedFile.md`](./TestLinkedFile.md) above, which takes it to the `tree/branch-name/path/to/file` style link, and then the `README.md` link in that file, which retains that sub-path.

  In this case, the link in the note block is rendered as expected (relative to the source tree).

## See Also

Github bug filed under <https://support.github.com/ticket/personal/0/2377367>
