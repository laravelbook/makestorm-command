#PhpStorm 6 Command Line Tool Builder

MIT license

This will create a [custom command line tool](http://www.jetbrains.com/phpstorm/webhelp/command-line-tool-support.html) for use by [PhpStorm 6](http://www.jetbrains.com/phpstorm/). I built it explicitly to invoke the Laravel 4 artisan commands, but it should work for any command line tool that uses the [Symfony 2.x Console component](https://github.com/symfony/Console) 

Very lightly tested on OSX Lion with PhpStorm 6. Should work on Linux or OSX or Windows.
Windows users may have to explicitly set the path to the PhpStorm prefs.
NOT tested even a little tiny bit on Windows of any flavor

###Usage:
Run in any directory:
```php makestorm.php <toolname> [OPTIONAL]-p<path to phpstorm prefs>```

FIRST, add a custom command line tool in PhpStorm 6: Preferences::Command Line Tool Support;

Click the '+' sign below the tool list and select 'Custom Tool';

To invoke the tool using php you'll need to add an alias for the executable:
   ```"$PhpExecutable$" /full/path/to/artisan```

Be sure to remember the "Tool Name" you assign.
PhpStorm will have created an 'empty' ```<toolname>.xml``` file in its prefs directory that we will populate.

Test the command tool in the Command Line Tools Console to make sure it runs
  usiing ```<command alias> list --xml```.
You should see quite a bit of XML output in the console listing all of the commands.

If not, the tool wasn't invoked correctly or it doesn't support XML output
...We parse this XML from 'list' to build the command line support file, and makestorm won't work without it. Sorry.

Now you should be able to just run ```php makestorm.php <toolname>``` from the command line.

Makestorm should find the path to the PhpStorm prefs folder and load the correct ```toolname.xml``` file that was created there.
If it can't you may need to explicitly point to it when you run makestorm.

See http://www.jetbrains.com/phpstorm/webhelp/project-and-ide-settings.html for normal locations.
Specify it like this: ```php makestorm.php <toolname> -p<path to phpstorm prefs>```

If you go back into PhpStorm to the Command Line Tool Support page, select your tool,
and reload it (click the little recycle button under the list).

You should be able to then invoke the tool using the alias you setup when you created it.
See http://www.jetbrains.com/phpstorm/webhelp/running-command-line-tool-commands.html

That's it.
