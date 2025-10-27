## Bash Commands
The following are frequently used `bash` commands. Most commands need a parameter to be provided. However, some can function with any parameter e.g. `ls`, `cd`, `pwd`, `tree`. Some commands have options with help you achieve unique results. Command options are provided by adding a hyphen followed by the option required.

1. `ls` - used to *list* files or folders in the current folder or a given path e.g.:
   - `ls` without any path parameter or options. will display files and folders in the current folders. It will output something similar to:
     
   - `ls -l` - demonstrates the use of the option `-l` for the command `ls`. It lists files in a long listing format in order to get more details on these files and folders. 

It will display or output something like the following:

     ```
     total 44
     drwxr-xr-x 2 jdoe jdoe  4096 Apr  9 19:53 bash
     drwxr-xr-x 2 jdoe jdoe  4096 Mar 28 12:32 git
     drwxr-xr-x 2 jdoe jdoe  4096 Oct 11 13:30 linux
     drwxr-xr-x 2 jdoe jdoe  4096 Oct 14 14:47 practicals
     drwxr-xr-x 2 jdoe jdoe  4096 Oct  9 19:33 python
     -rw-r--r-- 1 jdoe jdoe 10008 Apr  7 21:29 README.md
     drwxr-xr-x 2 jdoe jdoe  4096 Oct 17 17:02 sql
     drwxr-xr-x 2 jdoe jdoe  4096 Apr  9 19:40 supplemental
     drwxr-xr-x 4 jdoe jdoe  4096 Oct 15 12:09 util
     ```
   - Explanation of the above data and columns:
     - First column identifies whether the row represents a file or a folder and the file permissions. 
       - Anything beginning with a `d` is a directory/folders. Anything row beginning with a `-` is a file.
       - The next three(3) sets each of 3 characters after the `file/directory` character represent permissions for the `user`, `group` and `others` (ie anyone who is not the user and not in the group).
     - Second - indicates links to the current file.
     - Third - user who owns the file/directory.
     - Fourth - group that owns the file/directory.
     - Fifth - size of the file/directory.
     - Sixth - time at which the file/directory was last changed/modified.

   - `ls -a` - will list/display all files including hidden files/folders.
   - `ls -al` or `ls -la` - will list/display all files/folders in the long listing format and will include hidden file/directories. Note this is simply a way to combine the `-a` and `-l` options for the `ls` command.

The`man` command to find more information about the ls command by typing - `man ls`
- `ls` can also take a parameter e.g. the `path` to a file/folder if that `path` is valid. e.g.:
     - `ls Documents/git/mentor` - will list the files/folders in path parameter provided. NB: See the path section to better understand what a file/folder path is.

2. `cd` - is short for `change directory`. It allows the user to change from one directory/folder to another. e.g.
   - `cd` with no path parameter will change the current directory you to your home directory aka `~` or `/home/yourusername`.
   - `cd Documents/git/mentor/` will change the current directory to the `mentor` directory.
   - `cd ..` - changes to the parent directory of the current directory or one folder back in the path. e.g. if you are currently in `Documents/git/mentor/`, then `cd ..` will change to `Documents/git/

3. `pwd` - print working directory.
         It displays your current location.

4. `man` - help tool for any linux command. To get detailed help on a given command, type `man thecommandyouwishtofindoutmoreabout`

5. `grep` - prints lines that matches a pattern provided e.g.:
   - `grep Nate ~/Documents/git/mentor/.test.student.csv` - searches for the word `Nate` in the file path provided.

6. `cat` - concatenates 1 or more files and prints the output on the screen. Most people typically use this to display the internal contents of a file. However, if you have a file with hundreds of lines, this is not ideal for such. See the `less` command. e.g. of cat usage:
    - `cat ~/Documents/git/mentor/util/data/firstname` - will print out all the contents of the file `firstname`.
    - `cat ~/Documents/git/mentor/util/data/*` - will combine all the files in the folder `data` and print them out.

7. `less` - allows you to peruse a file a page at a time e.g. `less ~/Documents/git/mentor/.test.student.csv` - will display the first page. Additionally, it has search features to help you narrow down text. You can do the following:
    - Press `pg-down` or `pg-down` to quickly navigate through pages at a time.
    - Press `/` followed by some text that you wish to search and press enter.
    - Press `q` to exit.

8. `tail` - prints out the last 10 lines of a file. This can be adjusted to print more or less.

9. `head` - prints out the first 10 lines of a file. This can be adjusted to print more or less.

10. `cp` - copies files from a source to a destination folder e.g.:
    - `cp ~/Documents/git/mentor/.sampledata/31??_* ~/Documents/bash-sandbox/test_folder` - the wildcards can be used with any bash/zsh command. In this example all the files matching the path containing the wildcards will be copied to a folder called `test_folder` that's to be found inside the `bash-sandbox`
    - `cp -r ~/Documents/git/mentor/* ~/Documents/bash-sandbox/test_data/`. Copies all files and folders including subdirectories.

11. `find` - used to search for files in a directory hierarchy e.g:
    - `find ~/Documents/ -type f -name '*Zippy*'` - to search for files that contain `Zippy` in the file name.
    - `find ~/Documents/git/ -type d -name '*-*'` - to search for directories that contain `-` in the directory name.
12. `history`

13. `echo` - allows users to display lines of text or strings that are passed as arguments.
(>)-overwriter (>>)append operator 
    `echo" ">> filename`

14. `mkdir`- make directory. Allows users to create new directoies.

15. `mv`- used to move or rename files and directories.

16. `rm`- remove. Removing files which include special files such as directories from the file system. ` rm -r`

17. `sed`- stream editor. Used to perform basic text transformations on an input stream (quick edits).

18. `vi` - this could invoke the traditional `vi` or the improved (and recommended) vi referred to as `vim`.

19. `ssh-keygen`- this is a tool for creating new authentication key pairs for SSH. used for automating logins, sinle sign-on, and for authenticating hosts.

20. `tree`- maps directory structures in a hierachical, tree -like format.
             `tree`   `tree /home/lwachira/Documents/test`

21. `scp`- program for copying files between computers. Fetches a file from the remote host, and puts it in the directory indicated by path.

22. `rsync`- stands for remote synchronization. Synces files and folders between two hosts or machines.

23. `awk`- used for manipulating data and generating reports. By default it prints every line of data from the specified file.

24. `unzip`- used to extract files from zip archives, preservingdirectory structures and permissions.

25. `tar`- stands for tape archive. Bundles files and folders into a single archive while keeping their structure and permissions intact.

26. `wget`- Makes it possible to download files from the internet directly to your active directory. It operates in the background, allowing tasks to continue even if offline.
27. `curl`- Used for transfering data to or from a server, employing a range of internet protocols eg. HTTP, HTTPS, Scp.

28. `printf`- Used to display formatted text, numbers or other data types directly in the terminal.

# Questions

## Section 1: Using ONLY ls with Wildcards (*, ?) - No Pipes or grep


### TASKS.

**1. List all student data files (.txt files) in the .sampledata directory.**

 ``` ls *.txt ```

1001_Amber_C_Atieno.txt        2171_Johnson_C_Atieno.txt
1002_Amber_C_Chacha.txt        2172_Johnson_C_Chacha.txt
1003_Amber_C_Idris.txt         2173_Johnson_C_Idris.txt
1004_Amber_C_Kamau.txt         2174_Johnson_C_Kamau.txt
1005_Amber_C_Kimani.txt        2175_Johnson_C_Kimani.txt
1006_Amber_C_Kiptoo.txt        2176_Johnson_C_Kiptoo.txt
1007_Amber_C_Maribe.txt        2177_Johnson_C_Maribe.txt


**2. List all student data files where the student ID starts with 10 and ends with any two digits (e.g., 1001, 1005).**

``` ls 10??*```

1001_Amber_C_Atieno.txt    1034_Amber_K_Wanyonyi.txt  1067_Amber_P_Ouma.txt
1002_Amber_C_Chacha.txt    1035_Amber_K_Yegon.txt     1068_Amber_P_Ratemo.txt
1003_Amber_C_Idris.txt     1036_Amber_K_Yebo.txt      1069_Amber_P_Wambugu.txt
1004_Amber_C_Kamau.txt     1037_Amber_L_Atieno.txt    1070_Amber_P_Wanyonyi.txt
1005_Amber_C_Kimani.txt    1038_Amber_L_Chacha.txt    1071_Amber_P_Yegon.txt

1032_Amber_K_Ratemo.txt    1065_Amber_P_Nuru.txt      1098_Ami_C_Maxx.txt
1033_Amber_K_Wambugu.txt   1066_Amber_P_Otieno.txt    1099_Ami_C_Mulanga.txt

**3. List all student data files where the student ID starts with 10 and ends with either 2 or 7 (e.g., 1007, 1022).**

``` ls 10?[27]*```

1002_Amber_C_Chacha.txt   1037_Amber_L_Atieno.txt    1072_Amber_P_Yebo.txt
1007_Amber_C_Maribe.txt   1042_Amber_L_Kiptoo.txt    1077_Amber_W_Kimani.txt
1012_Amber_C_Otieno.txt   1047_Amber_L_Nuru.txt      1082_Amber_W_Mwangi.txt
1017_Amber_C_Yegon.txt    1052_Amber_L_Wanyonyi.txt  1087_Amber_W_Wambugu.txt

**4. List all student data files where the student ID is between 1100 and 1199.**

``` ls 11[0-9]*```

1100_Ami_C_Mwangi.txt    1134_Ami_L_Maxx.txt      1168_Ami_W_Kiptoo.txt
1101_Ami_C_Nuru.txt      1135_Ami_L_Mulanga.txt   1169_Ami_W_Maribe.txt
1102_Ami_C_Otieno.txt    1136_Ami_L_Mwangi.txt    1170_Ami_W_Maxx.txt
1131_Ami_L_Kimani.txt    1165_Ami_W_Idris.txt     1199_Alice_K_Atieno.txt
1132_Ami_L_Kiptoo.txt    1166_Ami_W_Kamau.txt
1133_Ami_L_Maribe.txt    1167_Ami_W_Kimani.txt

**5. List all student data files where the student's first name starts with 'A' or 'B'.**

``` ls ?????[AB]* ```

1001_Amber_C_Atieno.txt    1121_Ami_K_Ouma.txt        1241_Alice_P_Maribe.txt
1002_Amber_C_Chacha.txt    1122_Ami_K_Ratemo.txt      1242_Alice_P_Maxx.txt
1003_Amber_C_Idris.txt     1123_Ami_K_Wambugu.txt     1243_Alice_P_Mulanga.txt
1004_Amber_C_Kamau.txt     1124_Ami_K_Wanyonyi.txt    1244_Alice_P_Mwangi.txt
1117_Ami_K_Mulanga.txt     1237_Alice_P_Idris.txt     1357_Beth_W_Wambugu.txt
1118_Ami_K_Mwangi.txt      1238_Alice_P_Kamau.txt     1358_Beth_W_Wanyonyi.txt
1119_Ami_K_Nuru.txt        1239_Alice_P_Kimani.txt    1359_Beth_W_Yegon.txt
1120_Ami_K_Otieno.txt      1240_Alice_P_Kiptoo.txt    1360_Beth_W_Yebo.txt

**6. List all student data files where the student's middle initial is 'Z/L'.**

``` ls *_*_L_*```

1763_Joan_L_Maribe.txt         2567_Maryanne_L_Atieno.txt   3299_Zora_L_Ouma.txt
1764_Joan_L_Maxx.txt           2568_Maryanne_L_Chacha.txt   3300_Zora_L_Ratemo.txt
1765_Joan_L_Mulanga.txt        2569_Maryanne_L_Idris.txt    3301_Zora_L_Wambugu.txt
1766_Joan_L_Mwangi.txt         2570_Maryanne_L_Kamau.txt    3302_Zora_L_Wanyonyi.txt
1767_Joan_L_Nuru.txt           2571_Maryanne_L_Kimani.txt   3303_Zora_L_Yegon.txt
1768_Joan_L_Otieno.txt         2572_Maryanne_L_Kiptoo.txt   3304_Zora_L_Yebo.txt

**7. List all student data files where the student ID is between 1200 and 1299.**

``` ls 12[0-9]* ```

1200_Alice_K_Chacha.txt    1234_Alice_L_Yebo.txt      1268_Alice_W_Wanyonyi.txt
1201_Alice_K_Idris.txt     1235_Alice_P_Atieno.txt    1269_Alice_W_Yegon.txt
231_Alice_L_Wambugu.txt   1265_Alice_W_Ouma.txt      1299_Beth_K_Nuru.txt
1232_Alice_L_Wanyonyi.txt  1266_Alice_W_Ratemo.txt

**8. List all student data files where the student ID is between 1300 and 1399.**

``` ls 13[0-9]* ```

1300_Beth_K_Otieno.txt    1334_Beth_P_Mwangi.txt    1368_Conrad_C_Maxx.txt
1301_Beth_K_Ouma.txt      1335_Beth_P_Nuru.txt      1369_Conrad_C_Mulanga.txt
1302_Beth_K_Ratemo.txt    1336_Beth_P_Otieno.txt    1370_Conrad_C_Mwangi.txt
1330_Beth_P_Kiptoo.txt    1364_Conrad_C_Kamau.txt   1398_Conrad_L_Chacha.txt
1331_Beth_P_Maribe.txt    1365_Conrad_C_Kimani.txt  1399_Conrad_L_Idris.txt

**9. List all student data files where the student ID is between 1400 and 1499.**

``` ls 14[0-9]* ```

1400_Conrad_L_Kamau.txt     1434_Conrad_W_Chacha.txt    1468_Edward_C_Yebo.txt
1401_Conrad_L_Kimani.txt    1435_Conrad_W_Idris.txt     1469_Edward_K_Atieno.txt
1402_Conrad_L_Kiptoo.txt    1436_Conrad_W_Kamau.txt     1470_Edward_K_Chacha.txt
1430_Conrad_P_Wanyonyi.txt  1464_Edward_C_Ratemo.txt    1498_Edward_L_Otieno.txt
1431_Conrad_P_Yegon.txt     1465_Edward_C_Wambugu.txt   1499_Edward_L_Ouma.txt

**10. List all student data files where the student ID ends with a 0 (e.g., 1000, 1010).**

``` ls ???0* ```

1010_Amber_C_Mwangi.txt        1790_Joan_P_Wanyonyi.txt     2570_Maryanne_L_Kamau.txt
1020_Amber_K_Chacha.txt        1800_Joan_W_Maxx.txt         2580_Maryanne_L_Ratemo.txt
1030_Amber_K_Otieno.txt        1810_Joan_W_Yebo.txt         2590_Maryanne_P_Kiptoo.txt
1040_Amber_L_Kamau.txt         1820_Joanne_C_Mwangi.txt     2600_Maryanne_P_Wanyonyi.txt

**11. List all student data files where the student ID ends with a 5 (e.g., 1005, 1015).**

``` ls ???5* ```

1005_Amber_C_Kimani.txt       1785_Joan_P_Nuru.txt         2565_Maryanne_K_Yegon.txt
1015_Amber_C_Wambugu.txt      1795_Joan_W_Idris.txt        2575_Maryanne_L_Mulanga.txt
1025_Amber_K_Maribe.txt       1805_Joan_W_Ouma.txt         2585_Maryanne_P_Atieno.txt

**12. List all student data files where the third digit of the student ID is 2 (e.g., 102x, 112x).**

 ``` ls ??2?* ```

1020_Amber_K_Chacha.txt        1820_Joanne_C_Mwangi.txt     2620_Maryanne_W_Yebo.txt
1021_Amber_K_Idris.txt         1821_Joanne_C_Nuru.txt       2621_Nadia_C_Atieno.txt
1022_Amber_K_Kamau.txt         1822_Joanne_C_Otieno.txt     2622_Nadia_C_Chacha.txt

**13. List all student data files where the third digit of the student ID is 2 (e.g., 102x, 112x) AND their middle initial is L**

 ``` ls ??2?_*_L_* ```

1127_Ami_L_Atieno.txt     2027_Josh_L_Atieno.txt       2927_Okello_L_Atieno.txt
1128_Ami_L_Chacha.txt     2028_Josh_L_Chacha.txt       2928_Okello_L_Chacha.txt
1129_Ami_L_Idris.txt      2029_Josh_L_Idris.txt        2929_Okello_L_Idris.txt

**14. List all student data files where the fourth digit of the student ID is 5 (e.g., 1xx5).**

``` ls ???5* ```

1005_Amber_C_Kimani.txt       1785_Joan_P_Nuru.txt         2565_Maryanne_K_Yegon.txt
1015_Amber_C_Wambugu.txt      1795_Joan_W_Idris.txt        2575_Maryanne_L_Mulanga.txt
1025_Amber_K_Maribe.txt       1805_Joan_W_Ouma.txt         2585_Maryanne_P_Atieno.txt

**15. List all student data files where the second digit of the student ID is 0 (e.g., 10xx).**

``` ls ?0??* ```

1096_Ami_C_Kiptoo.txt      2096_Joshua_C_Wanyonyi.txt  3096_Yannis_K_Maxx.txt
1097_Ami_C_Maribe.txt      2097_Joshua_C_Yegon.txt     3097_Yannis_K_Mulanga.txt
1098_Ami_C_Maxx.txt        2098_Joshua_C_Yebo.txt      3098_Yannis_K_Mwangi.txt
1099_Ami_C_Mulanga.txt     2099_Joshua_K_Atieno.txt    3099_Yannis_K_Nuru.txt

**16. List all student data files where the last digit of the student ID is 9.**

``` ls ???9* ```

1759_Joan_L_Idris.txt         2539_Maryanne_C_Mulanga.txt  3319_Zora_P_Wambugu.txt
1769_Joan_L_Ouma.txt          2549_Maryanne_K_Atieno.txt   3329_Zora_W_Maribe.txt
1779_Joan_P_Kimani.txt        2559_Maryanne_K_Nuru.txt     3339_Zora_W_Yegon.txt

**17. List all student data files where the student ID is between 1000 and 1009.**

``` ls 100[0-9]* ```

1001_Amber_C_Atieno.txt  1004_Amber_C_Kamau.txt   1007_Amber_C_Maribe.txt
1002_Amber_C_Chacha.txt  1005_Amber_C_Kimani.txt  1008_Amber_C_Maxx.txt
1003_Amber_C_Idris.txt   1006_Amber_C_Kiptoo.txt  1009_Amber_C_Mulanga.txt


**18.List all student data files where the first name starts with 'N'.**

``` ls *_N*_* ```

2621_Nadia_C_Atieno.txt    2681_Nadia_P_Maribe.txt    2741_Nate_K_Ouma.txt
2622_Nadia_C_Chacha.txt    2682_Nadia_P_Maxx.txt      2742_Nate_K_Ratemo.txt
2623_Nadia_C_Idris.txt     2683_Nadia_P_Mulanga.txt   2743_Nate_K_Wambugu.txt
2624_Nadia_C_Kamau.txt     2684_Nadia_P_Mwangi.txt    2744_Nate_K_Wanyonyi.txt
2625_Nadia_C_Kimani.txt    2685_Nadia_P_Nuru.txt      2745_Nate_K_Yegon.txt

**19. List all student data files where the first name starts with 'O'**

``` ls *_O*_* ```

2857_Obadiah_P_Idris.txt     2917_Okello_K_Mulanga.txt    2977_Okello_W_Wambugu.txt
2858_Obadiah_P_Kamau.txt     2918_Okello_K_Mwangi.txt     2978_Okello_W_Wanyonyi.txt
2859_Obadiah_P_Kimani.txt    2919_Okello_K_Nuru.txt       2979_Okello_W_Yegon.txt

**20. List all student data files where the first name starts with 'M'.**

``` ls *_M*_*_* ```

2438_Martin_W_Wanyonyi.txt  2528_Mary_W_Wanyonyi.txt  2618_Maryanne_W_Wanyonyi.txt
2439_Martin_W_Yegon.txt     2529_Mary_W_Yegon.txt     2619_Maryanne_W_Yegon.txt
2440_Martin_W_Yebo.txt      2530_Mary_W_Yebo.txt      2620_Maryanne_W_Yebo.txt

**21. List all student data files where the first name starts with 'Z'**

``` ls *_Z*_*_* ```

3218_Zippy_P_Kamau.txt     3278_Zora_K_Mwangi.txt     3338_Zora_W_Wanyonyi.txt
3219_Zippy_P_Kimani.txt    3279_Zora_K_Nuru.txt       3339_Zora_W_Yegon.txt
3220_Zippy_P_Kiptoo.txt    3280_Zora_K_Otieno.txt     3340_Zora_W_Yebo.txt

**22. List all student data files where the middle initial is 'C'.**

``` ls *_*_C_* ```

1730_Joan_C_Mwangi.txt         2534_Maryanne_C_Kamau.txt    3266_Zora_C_Wanyonyi.txt
1731_Joan_C_Nuru.txt           2535_Maryanne_C_Kimani.txt   3267_Zora_C_Yegon.txt

**23. List all student data files where the middle initial is 'K'.**

``` ls *_*_K_* ```

748_Joan_K_Mwangi.txt         2552_Maryanne_K_Kamau.txt    3284_Zora_K_Wanyonyi.txt
1749_Joan_K_Nuru.txt           2553_Maryanne_K_Kimani.txt   3285_Zora_K_Yegon.txt
1750_Joan_K_Otieno.txt         2554_Maryanne_K_Kiptoo.txt   3286_Zora_K_Yebo.txt

**24. List all student data files where the middle initial is 'L'**

```ls *_*_L_*```
1037_Amber_L_Atieno.txt        2207_Johnson_L_Atieno.txt
1038_Amber_L_Chacha.txt        2208_Johnson_L_Chacha.txt
1039_Amber_L_Idris.txt         2209_Johnson_L_Idris.txt
1040_Amber_L_Kamau.txt         2210_Johnson_L_Kamau.txt

**25. List all student data files where the middle initial is 'P'.**

```ls *_*_P_*```
1055_Amber_P_Atieno.txt        2225_Johnson_P_Atieno.txt
1056_Amber_P_Chacha.txt        2226_Johnson_P_Chacha.txt
1057_Amber_P_Idris.txt         2227_Johnson_P_Idris.txt
1058_Amber_P_Kamau.txt         2228_Johnson_P_Kamau.txt

**26. List all student data files where the last name starts with 'R'.**

```ls *_*_*_R*```

1014_Amber_C_Ratemo.txt      2184_Johnson_C_Ratemo.txt
1032_Amber_K_Ratemo.txt      2202_Johnson_K_Ratemo.txt

**27. List all student data files where the last name starts with 'M'.**

```ls *_*_*_M*```

1007_Amber_C_Maribe.txt       2177_Johnson_C_Maribe.txt
1008_Amber_C_Maxx.txt         2178_Johnson_C_Maxx.txt
1009_Amber_C_Mulanga.txt      2179_Johnson_C_Mulanga.txt


**28.List all student data files where the last name starts with 'Y'.**

```ls *_*_*_Y*```

1017_Amber_C_Yegon.txt      2187_Johnson_C_Yegon.txt
1018_Amber_C_Yebo.txt       2188_Johnson_C_Yebo.txt
1035_Amber_K_Yegon.txt      2205_Johnson_K_Yegon.txt


**29.List all student data files where the last name ends with 'u'.**

``` ls *_*_*_*u*```

1004_Amber_C_Kamau.txt        2174_Johnson_C_Kamau.txt
1009_Amber_C_Mulanga.txt      2179_Johnson_C_Mulanga.txt
1011_Amber_C_Nuru.txt         2181_Johnson_C_Nuru.txt

**30. List all student data files where the last name contains 'on'.**

```ls *_*_*_*on*```

1016_Amber_C_Wanyonyi.txt      2186_Johnson_C_Wanyonyi.txt
1017_Amber_C_Yegon.txt         2187_Johnson_C_Yegon.txt
1034_Amber_K_Wanyonyi.txt      2204_Johnson_K_Wanyonyi.txt

**31.List all student data files where the student ID is between 1050 and 1059 AND the first name starts with 'A'.**

```ls {1050..1059}*_A*_*_*```  ```ls {1050..1059}*_A*_*_*```  ```ls 105*_A*_*_*```
1050_Amber_L_Ratemo.txt    1054_Amber_L_Yebo.txt    1058_Amber_P_Kamau.txt
1051_Amber_L_Wambugu.txt   1055_Amber_P_Atieno.txt  1059_Amber_P_Kimani.txt
1052_Amber_L_Wanyonyi.txt  1056_Amber_P_Chacha.txt
1053_Amber_L_Yegon.txt     1057_Amber_P_Idris.txt


**32. List all student data files where the student ID is between 1110 and 1119 AND the middle initial is 'K'.**

```ls {1110..1119}*_*_K_*```

1110_Ami_K_Chacha.txt  1113_Ami_K_Kimani.txt  1116_Ami_K_Maxx.txt     1119_Ami_K_Nuru.txt
1111_Ami_K_Idris.txt   1114_Ami_K_Kiptoo.txt  1117_Ami_K_Mulanga.txt
1112_Ami_K_Kamau.txt   1115_Ami_K_Maribe.txt  1118_Ami_K_Mwangi.txt


**33. List the student data file for 'Alice Otieno' (exact first and last name, any middle initial).**

```ls *_Alice_*_Otieno*```

1192_Alice_C_Otieno.txt  1228_Alice_L_Otieno.txt  1264_Alice_W_Otieno.txt
1210_Alice_K_Otieno.txt  1246_Alice_P_Otieno.txt

**34. List all student data files where the first name starts with 'C' AND the middle initial is 'D/C'.**

 ```ls *_C*_C_*```

1361_Conrad_C_Atieno.txt  1367_Conrad_C_Maribe.txt   1373_Conrad_C_Ouma.txt
1362_Conrad_C_Chacha.txt  1368_Conrad_C_Maxx.txt     1374_Conrad_C_Ratemo.txt
1363_Conrad_C_Idris.txt   1369_Conrad_C_Mulanga.txt  1375_Conrad_C_Wambugu.txt
1364_Conrad_C_Kamau.txt   1370_Conrad_C_Mwangi.txt   1376_Conrad_C_Wanyonyi.txt
1365_Conrad_C_Kimani.txt  1371_Conrad_C_Nuru.txt     1377_Conrad_C_Yegon.txt
1366_Conrad_C_Kiptoo.txt  1372_Conrad_C_Otieno.txt   1378_Conrad_C_Yebo.txt

**35. List all student data files where the student ID is 10?? (any two digits after 10) AND the last name ends with 's'.**

```ls 10??_*_*_*s*```

1003_Amber_C_Idris.txt  1039_Amber_L_Idris.txt  1075_Amber_W_Idris.txt
1021_Amber_K_Idris.txt  1057_Amber_P_Idris.txt  1093_Ami_C_Idris.txt

## Section 2: Use grep ,find for Advanced Search.

**1. Find all student data files (.txt) that contain the word "Mathematics" (case-sensitive).**

```find . -name "*.txt" -exec grep "Mathematics" {} +```

./2400_Martin_L_Ratemo.txt:Mathematics;69.2215
./1852_Joanne_L_Kiptoo.txt:Mathematics;57.4500
./1697_James_P_Ouma.txt:Mathematics;64.4143

**2. Find all student data files (.txt) where the student's email address ends with @hotmail.com.**

```find . -name "*.txt" -exec grep "@hotmail.com" {} +```

./3044_Rachel_P_Mwangi.txt:Email: rpmwangi@hotmail.com
./3154_Yannis_W_Otieno.txt:Email: ywotieno@hotmail.com

**3. Count how many student data files contain the phrase "CountyNum: 1".**

```find . -name "*.txt" -exec grep "CountyNum: 1$" {} + | wc -l```

```64```
 - wc - word count 
 - l - line count option 
 - $ - end of line

**4. List the names (full path) of all student data files (.txt) that have a score of 99 for any subject**

```find . -name "*.txt" -exec grep ";99" {} + | xargs realpath```
 
/home/lwachira/Documents/git/quatrix-mentor/.sampledata/2115_Joshua_K_Yegon.txt:Mathematics;99.6062
/home/lwachira/Documents/git/quatrix-mentor/.sampledata/1631_James_C_Atieno.txt:Physics;99.2595

-  xargs - takes input (usually from a pipe) and converts it into arguments for another command. It takes a list of things and gives them to another command to use. 

**5. Find all student data files (.txt) that contain the name "Alice" (case-insensitive).**

```find . -name "*.txt" -exec grep "Alice" {} +```

./1212_Alice_K_Ratemo.txt:Name: Alice K. Ratemo
./1269_Alice_W_Yegon.txt:Name: Alice W. Yegon
./1189_Alice_C_Mulanga.txt:Name: Alice C. Mulanga

**6.Find all student data files (.txt) that were created within the last 24 hours (assuming you just ran generate_data.sh).**

```find . -name "*.txt" -mtime -10```

./2400_Martin_L_Ratemo.txt
./1852_Joanne_L_Kiptoo.txt
./1697_James_P_Ouma.txt
./3044_Rachel_P_Mwangi.txt
-  -mtime -10 list files creates in less than 10 days. No file was created within the last 24 hours. 
  - To check time modified: 

  ```stat ./1761_Joan_L_Kimani.txt```

  Size: 175       	Blocks: 8          IO Block: 4096   regular file
Device: 259,2	Inode: 4591709     Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1007/lwachira)   Gid: ( 1007/lwachira)
Access: 2025-10-22 10:43:34.431412366 +0300
Modify: 2025-10-13 11:25:04.434598279 +0300
Change: 2025-10-13 11:25:04.434598279 +0300

**7. Find all student data files (.txt) that are larger than 200 bytes.**

```find . -name "*.txt" -size +200c```

./1697_James_P_Ouma.txt
./3044_Rachel_P_Mwangi.txt
./2519_Mary_W_Maribe.txt
 - Kilobytes - +200K
- Megabytes - +200M
- Gigabytes - +200G

**8. Find all .csv files in the current directory that contain the word "Nairobi".**

```find . -name "*.csv" -exec grep "Nairobi" {} +```
./.test.county.csv:47;Nairobi
./.test.school.csv:231;47;Nairobi - National
./.test.school.csv:232;47;Nairobi - Provincial
./.test.school.csv:233;47;Nairobi - District

**9. List all student IDs (the 4-digit number) from student data files that have "Physics" listed as a subject**

```find . -name "*.txt" -exec grep -l "Physics" {} + | xargs grep "Id"```

./.sampledata/2400_Martin_L_Ratemo.txt:Id: 2400
./.sampledata/1697_James_P_Ouma.txt:Id: 1697

```grep -r -B 10 "Physics" | grep -A 10 "Id"```

**10. Find all student data files (.txt) that contain the word "Email:" AND "CountyNum: 5".**

```find . -name "*.txt" -exec grep -l "Email" {} + | xargs grep "CountyNum: 5"```

./.sampledata/2400_Martin_L_Ratemo.txt:CountyNum: 5
./.sampledata/2598_Maryanne_P_Ratemo.txt:CountyNum: 5
./.sampledata/3254_Zora_C_Kamau.txt:CountyNum: 5

```grep -r -B "Email" | grep -A 1 "CountyNum: 5"```