Jekyll/GH-Pages
---------------


Install Ruby and Jekyll (on macOS)
-----------------------
 - Ref: https://jekyllrb.com/docs/installation/macos/

 - Install Ruby (Jekyll requires ruby > 2.5.0)

    ```
        brew install ruby
    ```

 - Add brew installed Ruby to `PATH`

    ```
        echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_login
    ```

 - Install Jekyll

    ```
        gem install --user-install bundler jekyll
    ```

 - Add gem installed Jekyll to `PATH`

    ```
        echo 'export PATH="$HOME/.gem/ruby/2.7.0/bin:$PATH"' >> ~/.bash_login
    ```

 - Check gem paths are setup correctly (look at `GEM PATHS:`)

    ```
        gem env
    ```

Create (new) Jekyll Site
------------------------

 - Ref: https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll

 - This is user site, so placing docs in `master` branch (see other options
   for projects/orgs, and related `gh-pages` branch).

 - Run jekyll new

    ```
        jekyll new .
    ```

    - NOTE: I had to remove `index.html` and `README.md` I had in local dir
      in order for this to allow me to create the `naughtont3.github.io`
      site.  Presumably I could have use `--force`.

 - Follow directions here...
    - https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll#creating-your-site

    - **NOTE** I also installed `gem install github-pages`

 - I had to edit `Gemfile` and set `github-pages` to version `204`,
   based on https://pages.github.com/versions/

 - Later I had to `gem update` to resolve dependency problem

 - Then I could start a local server to test site

    ```
        bundle exec jekyll serve
    ```

 - Then point browser at server address on localhost

    ```
        http://127.0.0.1:4000
    ```

Next Steps
----------

 - TODO: Start customizing the actual page from this default, and then view
   changes with embedded local server (`bundle exec jekyll serve`)


