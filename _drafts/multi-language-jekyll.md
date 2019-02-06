Reference links
http://chocanto.me/2016/04/16/jekyll-multilingual.html
https://forestry.io/blog/creating-a-multilingual-blog-with-jekyll/

No-gems method to build a multilanguage jekyll website

-my site is default en, and has a baseurl for portuguese.

Steps
- Create a languages.yml file inside _data
- Define the languages you will support and set the some properties to then(name/code/base).
- Define what pages you will translate fully (usually when there is a link inside, posts)and the ones that just some content(when its a line or a paragraph).
- Create a translations.yml file inside _data
- Config your translations to your selected languages. mine EN/PT
- Create a front matter 'lang' on your pages/posts to define in what language the file is rendered
- Create a front matter 'ref' on your pages/posts to identify the sinbling pace. Use its value in your base langugae
- Create a language-box fix inside _includes/ and the respective .sass file to work as language selection buttons
- refactor your code to get translated data from translations.yml;Test using the language buttons
- Create a pt(your alternative language) folder with pages and _posts folder inside. All files must be translated or getting data dynamicaly from _data. File title should be in pt.
- Config Disqus to use ref to store comments

I still dont know to to put pages and posts together inside jekyll, so my language-box is conditional to that.
