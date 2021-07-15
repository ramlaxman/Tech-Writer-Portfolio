# Install Jekyll on Windows in 15 minutes

Jekyll is a Ruby Gem that can be installed on most systems.

### Requirement
- `Ruby` version 2.4.0 or higher, including all development headers (check your Ruby version using ruby -v)
- `RubyGems` (check your Gems version using gem -v)
- `GCC` and `Make` (check versions using gcc -v,g++ -v, and make -v)

### Installation Steps

1. Download and install **`Ruby + Devkit latest version (x64).exe`** installer for Jekyll installation.
2. Just press `Enter` when ask to install **`ridk`** for `[1,3]` option.
3. Install the jekyll and bundler gems.
    ```
    gem install jekyll bundler
    ```
4. Create a new Jekyll site at `./myblog`.
    ```
    jekyll new myblog
    ```
    ![](https://github.com/ramlaxman/Tech-Writer-Portfolio/raw/main/Developer%20and%20Configuration%20Guides/Jekyll%20install%20steps/jek-1.PNG)
5. Change into your new directory.
    ```
    cd myblog
    ```
6. Build the site and make it available on a local server.
    ```
    bundle exec jekyll serve
    ```
    ![](https://github.com/ramlaxman/Tech-Writer-Portfolio/raw/main/Developer%20and%20Configuration%20Guides/Jekyll%20install%20steps/jek-2.PNG)

---
>
> **Note:** 
>  
> After step 4, you'll get an error message as follows: 
> ```
> C:/Ruby30-x64/lib/ruby/gems/3.0.0/gems/jekyll-4.2.0/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file --webrick (LoadError)
> ```
> To resolve this issue, simply run following command in command prompt:
> 
> `C:\> bundle add webrick`
> 
> It'll install gem for webrick.
> 
> ![](https://github.com/ramlaxman/Tech-Writer-Portfolio/raw/main/Developer%20and%20Configuration%20Guides/Jekyll%20install%20steps/jek-3.PNG)
> 
> If you're interested in more detail, you can check this GitHub [issue](https://github.com/jekyll/jekyll/issues/8523#issuecomment-751409319)
>  

Now, repeat the step 4.

![](https://github.com/ramlaxman/Tech-Writer-Portfolio/raw/main/Developer%20and%20Configuration%20Guides/Jekyll%20install%20steps/jek-4.PNG)

7. Browse to http://localhost:4000

Now, Jekyll website is live on localhost.
