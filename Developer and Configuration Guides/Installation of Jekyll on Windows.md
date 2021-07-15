# Install Jekyll on Windows in 15 minutes

Jekyll is a Ruby Gem that can be installed on most systems.

### Requirement
- `Ruby` version 2.4.0 or higher, including all development headers (check your Ruby version using ruby -v)
- `RubyGems` (check your Gems version using gem -v)
- `GCC` and `Make` (check versions using gcc -v,g++ -v, and make -v)

1. Install the jekyll and bundler gems.
    ```
    gem install jekyll bundler
    ```
2. Create a new Jekyll site at `./myblog`.
    ```
    jekyll new myblog
    ```
3. Change into your new directory.
    ```
    cd myblog
    ```
4. Build the site and make it available on a local server.
    ```
    bundle exec jekyll serve
    ```
5. Browse to http://localhost:4000

    > Note: On Windows, you will get error message as follows: 
    ```
    C:/Ruby30-x64/lib/ruby/gems/3.0.0/gems/jekyll-4.2.0/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)
    ```
    To resolve this issue, simply run following command on Windows:

    `C:\> bundle add webrick`

    If you're interested in more details, you can check (here

    It'll install gem for webrick.

    Now rerun step 4 and 

