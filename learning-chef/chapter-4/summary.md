# Write Your First Chef Recipe

## Hello World

As every time we learn new tools or programming language, let's start with a Hello World program. This simple Hello World script that we are going to create will show the basics of Chef. Let's start by writing a file named `hello.rb` and fill it with this block of code:

```
file 'hello.txt' do
  content 'Welcome to Chef'
end
```

Above, we define a file **resource** with path `hello.txt`. Inside a resource, we can define **attributes**. For the time being, it's suffice to say that attributes are description of desired configurations of our resources. In the case of our file above, we define that the desired configuration of our `hello.txt` file is to have 'Welcome to Chef' string as its content. To have Chef perform actions required to achieve the desired configurations we specified in `hello.rb`, we run command `chef-apply hello.rb`. The result should look like this in Mac:

```
Recipe: (chef-apply cookbook)::(chef-apply recipe)
  * file[hello.txt] action create
    - create new file hello.txt
    - update content in file hello.txt from none to 40a30c
    --- hello.txt 2018-05-08 06:19:13.569820688 +0530
    +++ ./.chef-hello20180508-8165-1rxp6g3.txt  2018-05-08 06:19:13.569488582 +0530
    @@ -1 +1,2 @@
    +Welcome to Chef
```

As you may also have noticed from the result above, `hello.rb` is our first **recipe**. A recipe is a file that contains Chef code.


## Recipes Specify Desired Configuration

As we can see from our `hello.rb`, Chef code uses a *domain-specific language* (DSL) built on top of Ruby programming language. Chef DSL is designed to make us focus more on describing what the desired configuration of a machine should be rather than how it should be accomplished. In our `hello.rb`, as explained in previous chapter, we defined a file resource. Resources are building blocks that Chef uses to configure things on a system. Within the file resource block in our code above, we then defined a content attribute. Having defined these configurations, we then let Chef to to decide how to put the system in the desired configuration by reasoning about the current state of the system. Chef determines what actions it should perform automatically and autonomously.

To make a more concrete example of how this principle actually works, let's try to run the command `chef-apply hello.rb` one more time. The result should look like this:

```
Recipe: (chef-apply cookbook)::(chef-apply recipe)
  * file[hello.txt] action create (up to date)
```

As we can see from the result above, since the current state of our system already satisfies the desired configurations we defined in `hello.rb`, Chef does not need to perform any additional actions. Now, let's try something more interesting. If we manually edit our `hello.txt` file by replacing its content with 'Modified outside of chef-apply' string and then we run `chef-apply hello.rb` one more time, we should see a result like this:

```
Recipe: (chef-apply cookbook)::(chef-apply recipe)
  * file[hello.txt] action create
    - update content in file hello.txt from bdbe83 to 40a30c
    --- hello.txt 2018-05-08 06:48:45.443128877 +0530
    +++ ./.chef-hello20180508-8451-kcsvib.txt 2018-05-08 06:49:59.532923365 +0530
    @@ -1,2 +1,2 @@
    -Modified outside of chef-apply
    +Welcome to Chef
```

Chef automatically and auotomously replace 'Modified outside of chef-apply' that we manually edited earlier with 'Welcome to Chef' string as specified in `hello.rb`. This is how Chef prevents *configuration drifts*.

## To Uninstall, Specify What Not to Do

Is it possible for Chef to automatically uninstall everything it installs? Not quite. However, we can perform the equivallent of uninstallation by telling CHef explicitly what not to do.


