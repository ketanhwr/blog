---
layout:     post
title:      Sublime Text for Competitive Programming
date:       2016-06-28 15:31:19
summary:    Custom C++ Build System for Linux/Mac users to compile and run directly in Sublime Text.
categories: competitive sublimetext
---

[Sublime Text](https://www.sublimetext.com/) is one of the most popular text editor these days. Its shortcuts, user interface, plugins and themes are responsible for its incredible popularity among programmers.

[Package Control](https://packagecontrol.io/) is the most popular package manager for Sublime Text. You can setup plugins, color schemes, themes, etc. easily after installing Package Control. (Check its website for instructions)

I currently use the beautiful [Brogrammer Theme](https://packagecontrol.io/packages/Theme%20-%20Brogrammer) and a few plugins along with it. This is how the UI was when I was debugging my code once.

<img src="{{ site.basurl }}/images/brogrammer.png" alt="Couldn't Load Image" />

_I was not able to find any error in my code so I made `generator.cpp` to generate random test cases and `brute.cpp` to generate an output file from the test cases using brute force. I then cross checked the output from my code's output. Yeah, I know, but it worked._

### Compiling and Running
As a competitive programmer, I am always looking for ways to code and test faster. This helps a lot when you are participating in contests where time matters a lot (Codeforces, for example). So as an Ubuntu user, I don't like it when I have to open Terminal everytime and type this:

{% highlight bash %}
g++ randomFile.cpp -o randomFile
./randomFile
{% endhighlight %}

Sublime Text has the power of building too! The Build System 'C++ Single File' works like a charm but it fails to work when you want to give some input from stdin. So after experimenting with the 'Custom Build System' tool, I made a custom Build System. In the 'Build System', choose 'New Build System...' and enter the following JSON data in the newly opened file.

_Note: This might not work for Mac users. Read the next section for this._

{% highlight json %}
{
  "cmd": ["g++", "-std=c++0x", "$file", "-o", "${file_path}/${file_base_name}"],
  "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
  "working_dir": "${file_path}",
  "selector": "source.c, source.c++, source.cxx, source.cpp",
  "variants": 
  [ 
    {
      "name": "Run",
      "cmd": ["bash", "-c", "g++ -std=c++0x '${file}' -o '${file_path}/${file_base_name}' &&  xterm -e bash -c '${file_path}/${file_base_name}; read'"]  
    }
  ]    
}
{% endhighlight %}

Save it by some random name and now choose that Build System for building it. Now `Ctrl+Shift+b` will give you the option to compile and run the file you just wrote.

For copying and pasting test cases into the terminal, copy it first from your source, and then in the terminal use `Shift+Insert` to paste in into the terminal.

_Note: You can change the terminal from `xterm` to any other of your choice as well._

### Mac Users
_(This will work for Linux users too.)_

If the above mentioned method did not work, then there is another way of providing input to your code!

[Sublime Input](https://packagecontrol.io/packages/Sublime%20Input) is a very popular plugin that provides input to your program via comments. This works for other languages as well!

For Sublime Input, choose 'C++ Single File' as your Build System. And to provide input, add your input as comment and then run it! _For Mac users, `Command+Ctrl+b` will do the trick._

Here is a sample C++ code that uses Sublime Input plugin.

{% highlight cpp %}
/*input
42
*/

#include <iostream>

int main()
{
	int n;

	std::cin >> n;
	std::cout << "You entered: " << n << "\n";

	return 0;
}
{% endhighlight %}

If you now run the program, you will see `You entered: 42` in the Sublime Text console.

### What about Windows users?
You can also setup Custom Build Systems in Windows. I have tried a lot tweaking with it in Windows and I was finally able to get Command Prompt up and running with my code. But that was a long time ago, so I have lost that `.build-system` file. I'll add the JSON data for Windows Build System too as soon as I get it up and running.

### Build System for other languages
You can go through these links for more knowledge about Custom Build Systems in Sublime Text:

* [http://docs.sublimetext.info/en/latest/reference/build_systems.html](http://docs.sublimetext.info/en/latest/reference/build_systems.html)
* [https://addyosmani.com/blog/custom-sublime-text-build-systems-for-popular-tools-and-languages/](https://addyosmani.com/blog/custom-sublime-text-build-systems-for-popular-tools-and-languages/)

### Some other overkills?
There are too many shortcuts in Sublime Text! You can read about some of them here:
[https://gist.github.com/eteanga/1736542](https://gist.github.com/eteanga/1736542)

### Other Text Editors?
These are other popular text editors and IDEs, competitive programmers use:

* Vim (Very popular due to many shortcuts and plugins)
* Emacs
* Code::Blocks (Compiles and runs without any problems)
* Gedit
* Visual Studio
* Notepad++
* Geany

#### P.S.: It is always better to solve more questions than solving easy questions very fast.