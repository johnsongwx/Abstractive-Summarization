# Install ROUGE&pyrouge in macOS/Ubuntu

Install in Ubuntu could check this：https://blog.csdn.net/wr339988/article/details/70165090

Install in macOS is simpler, check this：https://blog.csdn.net/baobao3456810/article/details/83744570

To sum up the steps:

Install perl - Install relative packages - Install ROUGE - Install pyrouge

Here are the problems I met:

### 1.

I forgot to use `sudo` when installing XML::DOM, which might cause errors later. If you want to uninstall packages related to perl, use

```bash
sudo cpanm --uninstall“$ module”
```

Detail：http://cn.voidcc.com/question/p-tbbfynbu-yu.html

Use this to check what you've installed:

```bash
perldoc perllocal
```

This isn't over. After you uninstall the packages, if you look at the installed packages list, you might find out they are still there. The perllocal info will not be updated simultaneously. Change "perllocal.pod" file by yourself.

 It is located in `/usr/local/Cellar/perl/5.32.0/lib/perl5/5.32.0/darwin-thread-multi-2level/perllocal.pod`

Detail:

http://cn.voidcc.com/question/p-tbbfynbu-yu.html

https://blog.csdn.net/linbian1168/article/details/90679919

### 2.

DEBUGs

Follow the instructions by the article I memtioned before, you might need this.

After running this command,

```bash
perl runROUGE-test.pl
```

You might meet this error.

> Can't locate XML/DOM.pm in @INC (you may need to install the XML::DOM module) (@INC contains: /Library/Perl/5.18/darwin-thread-multi-2level /Library/Perl/5.18 /Network/Library/Perl/5.18/darwin-thread-multi-2level /Network/Library/Perl/5.18 /Library/Perl/Updates/5.18.4/darwin-thread-multi-2level /Library/Perl/Updates/5.18.4 /System/Library/Perl/5.18/darwin-thread-multi-2level /System/Library/Perl/5.18 /System/Library/Perl/Extras/5.18/darwin-thread-multi-2level /System/Library/Perl/Extras/5.18 .) at ../ROUGE-1.5.5.pl line 173.
>
> BEGIN failed--compilation aborted at ../ROUGE-1.5.5.pl line 173.

开始我推测是XML::DOM安装过程中没有sudo，结果发现卸载重装以后还是不对。后来找到解决方案如下：

Type `where perl` in terminal, copy the FIRST location appeared below, and open `ROUGE-1.5.5.pl` & `runROUGE-test.pl`, change the first line's location by it.

### 3.

If you meet this error:

> ../ROUGE-1.5.5.pl -e ../data -c 95 -2 -1 -U -r 1000 -n 4 -w 1.2 -a ROUGE-test.xml > ../sample-output/ROUGE-test-c95-2-1-U-r1000-n4-w1.2-a.out
>
> Cannot open exception db file for reading: ../data/WordNet-2.0.exc.db

Open terminal and input:

```bash
cd /Users/gwx/Documents/rouge-evaluation/ROUGE-RELEASE-1.5.5/data
```

```bash
rm WordNet-2.0.exc.db
```

```bash
./WordNet-2.0-Exceptions/buildExeptionDB.pl ./WordNet-2.0-Exceptions ./smart_common_words.txt ./WordNet-2.0.exc.db
```

-------

DONE!
