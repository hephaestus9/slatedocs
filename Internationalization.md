[PR #1005](https://github.com/lord/slate/pull/1005) contained some suggestions for how to internationalize your site, using Middleman's [internationalization features](https://middlemanapp.com/advanced/localization/). If you pull that change into your tree, you can follow the instructions kindly provided by @benzookapi:

1.  Follow the middleman i18n steps, create the directory "localizable" under the "source" and move "index.html.md" there and create the directory "locales" under the root and put your target message files (e.g. "en.yml", "ja.yml"...)  The details is:  https://middlemanapp.com/advanced/localization/
(This is not included by my PR, done by users)

2. Embed "t(:YOUR_MESSAGE_KEY)" in index and other included .md files to where you want to i18n.
    e.g.
```
index.html.md
    title: t(:title)
--
en.yml
  en:
    title: "My Title"
--
ja.yml
  ja:
    title: "私のタイトル"
```
3.  now you can see "My title" in "YOUR_URL/en" and "私のタイトル" in "YOUR_URL/ja". How you can manage the path for localization is fully controlled by middle man i18n above.

4. This localization is applied to HTML title and page content and footers. 