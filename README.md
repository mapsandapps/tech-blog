# Running

Run with drafts visible: `hugo server -D`


Update theme: `git submodule update --remote --merge`


# New Post
`hugo new --kind post-bundle posts/my-post`

or maybe

`hugo new posts/my-first-post.md`

if there won't be any images.

Don't use `#` H1's. The post title will be a H1.

Change `draft: true` to `draft: false` at the top of the post to publish it on the next build

# Build

`hugo -D`

Output will be in ./public

# Info

Theme: [LoveIt](https://github.com/dillonzq/LoveIt)

Docs: [LoveIt docs](https://hugoloveit.com/categories/documentation/)

[Info banners](https://hugoloveit.com/theme-documentation-extended-shortcodes/#4-admonition)
