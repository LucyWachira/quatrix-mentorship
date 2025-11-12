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

`find . -name "*.txt" -exec grep ";99" {} + | xargs realpath`
 
```
/home/lwachira/Documents/git/quatrix-mentor/.sampledata/2115_Joshua_K_Yegon.txt:Mathematics;99.6062
/home/lwachira/Documents/git/quatrix-mentor/.sampledata/1631_James_C_Atieno.txt:Physics;99.2595
```

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

## Regular Expressions - RegEx
Regular expressions (popularly referred to as simply RegEx) are patterns that describes a set of strings that matches the pattern. This is helpful when:

- Searching for patterns in large files or data sets
- Replacing text/strings in large data sets that's hard to do with a simple Find and replace function.

## RegEx Metacharacters & Literals
buzz123 - any alpha-numeric set of characters are matched as they are eg in this case a RegEx pattern such as this will try to match any occurrence of the literal set of characters buzz123 in a given string.

1. ```.``` the dot - represents any character eg a-z, A-Z, 0-9, and special characters
2. ```^``` the carret symbol or character - represents beginning of the line. However when inside a square bracket, negates whatever characters are inside the square bracket.
3. ```$``` the carret symbol or character - represents end of the line.
4. ```?``` question mark - represents a non-greedy match for the preceeding regex pattern.
5. ```*``` asterisk or star. Represents 0 or more occurences of what preceeds the character eg.
.* - match any character if it occurs 0 or more times.
f* - match f 0 or more times
6. ```+``` plus or addition sign. Represents 1 or more occurences of what preceeds the character eg.
.+ - match any character if it occurs 1 or more times.
f+ - match f 1 or more times
7. ```|``` - vertical bar. This represents an or condition eg a|b will match if either an a or b character is present in the string. NB: This should not be confused with the bash or zsh command line pipe that has a different effect.
8. ```[]``` - square brackets. Matches a set of characters inside it. eg [abc] matches any occurrence of a, b or c. When a carret is used inside the square brackets eg [^abc] matches any character except a, b or c.
9. ```{}``` - curly brackets. Used to indicate precisely how many occurences you wish to match. eg
z{1} - matches 1 occurences of the character z
z{1,} - matches 1 or occurences of the character z
z{2,} - matches 2 or occurences of the character z
z{2,4} - matches 2 to 4 occurences of the character z
10. ```()``` - capture groups enclosed using regular brackets. A lot of use cases for regex revolve around search and replace. In order to re-use a successful matched patterns results, it is usually very helpful to take that result and use it in the final replace parameter. eg

You have a list of countries:
- Kenya
- Uganda
- Tanzania

(Ken)ya - will capture Ken
(\d{3}).* - capture Ken, Uga, and Tan. Try the above using online RegEx tester Regex101. Copy and paste the above text to Regex101 inside the TEST STRING field. To try our a regex pattern, enter it into the REGULAR EXPRESSION FIELD.
11. ```\``` - front-slash or used to preceed a special character that you wish to escape. Special symbols/characters need to be escaped eg:
\. - in this case, the dot is escaped and therefore the dot is treated as simple a dot and not representing any character
\? - the question mark is escaped. Therefore instead of being treated as a non-greedy indicator, it is matched to the actual question mark.

## Basic RegEx
Using the file .test.student.csv and .test.student.subject.csv using gedit or Text Editor or kwrite or VS Code and taking advantage of its regex feature, find all students with:

1. Last name Atieno
- Using Vs Code (ctrl+f)

```^\d+;\w+\s\w\sAtieno;.*```

2. Phone number for Airtel ie 073XX.
```^\d+;\w+\s\w\s\w+;(073)\d+.*```

3. From Tharaka Nithi ie county number 13. Use .test.student.csv file for this
```^\d+;\w+\s\w\s\w+;\d+\W\d+\W\d+;13```

4. From Nakuru that got 50% and above.
5. Email address that are either @gmail or @email.com.
```^\d+;\w+\s\w\s\w+;\d+\W\d+\W\d+;\d+;\w+@(gmail|email)\.com```

#### Repeat the above using:

1. grep to find all students with last name Atieno.

`grep -E "Atieno;" .test.student.csv`
```
1001;Amber C Atieno;0769-699-891;36;203;acatieno@yahoo.com
1019;Amber K Atieno;0720-548-173;2;142;akatieno@hotmail.com
1037;Amber L Atieno;0783-364-995;21;142;alatieno@hotmail.com
1055;Amber P Atieno;0720-022-522;13;26;apatieno@hotmail.com
```

2. grep to find Phone number for Airtel ie 073XX

`grep -E ";073[0-9\-]+;" .test.student.csv`
```
1007;Amber C Maribe;0739-960-684;23;118;acmaribe@hotmail.com
1008;Amber C Maxx;0730-690-514;41;67;acmaxx@email.com
1018;Amber C Yebo;0732-383-465;32;110;acyebo@hotmail.com
1021;Amber K Idris;0736-403-402;20;159;akidris@hotmail.com
```

3. grep to find: From Tharaka Nithi ie county number 13.

`grep -E ";13;" .test.student.csv`
```
1030;Amber K Otieno;0771-891-499;13;55;akotieno@gmail.com
1045;Amber L Mulanga;0788-421-002;13;146;almulanga@gmail.com
1055;Amber P Atieno;0720-022-522;13;26;apatieno@hotmail.com
1095;Ami C Kimani;0728-865-407;13;54;ackimani@gmail.com
1208;Alice K Mwangi;0757-262-208;13;160;akmwangi@yahoo.com
1240;Alice P Kiptoo;0719-821-652;13;65;apkiptoo@gmail.com
```

4. grep to find: Email address that are either @gmail or @email.com.

`grep -E "(@gmail|@email)\.com" .test.student.csv`
```
1003;Amber C Idris;0763-360-956;16;225;acidris@email.com
1004;Amber C Kamau;0704-852-218;8;149;ackamau@email.com
1006;Amber C Kiptoo;0784-567-283;19;142;ackiptoo@gmail.com
1008;Amber C Maxx;0730-690-514;41;67;acmaxx@email.com
1009;Amber C Mulanga;0753-068-016;25;51;acmulanga@email.com
```


1. less to: find all students with last name Atieno.

```less -p "Atieno;" .test.student.csv ```

2. less to find Phone number for Airtel ie 073XX.

```less -p "073[0-9\-]+" .test.student.csv ```

3. less to find: From Tharaka Nithi ie county number 13.

```less -p ";13;" .test.student.csv ```

4. less to find: Email address that are either @gmail or @email.com.

`less -p "(@gmail|@email)\.com" .test.student.csv`

## Advanced RegEx

Presented with the following data set of id, name, phone (Kenyan):
E.g
```
2956;Yannis C Atieno;(0775)-705-148
2957;Yannis C Chacha;0731-485430
2958;Yannis C Idris;786-408-485
2959;Yannis C Kamau;0700-823-247
```

You realize the phone numbers are not uniformly formatted. You are then tasked to reformat the above data so that:

It conforms to the following format eg:
2956;Yannis C Atieno;+254775705148
2957;Yannis C Chacha;+254731485430

1. That is, add the prefix +254 and remove characters such as (, ), - or spaces.

`;\(?0?(\d{3,})\)?[\s-]?(\d{3})[\s-]?(\d{3})`

replace : `+254$1$2$3`
###### Solution:
- \(?-....)?- to capture the phone number that starts with (0775).
- 0?- to capture the phone number that starts with 0. since not all numbers starts with 0 we have to add the ? for optionality.
- (\d{3,})- the fisrt capture group and since there is a number with more than 3 digits i have to add the(3,) e.g 254794-
- [\s-]?- to match the space and the hyphen but its optional(?) since not all numbers are seperated by a hyphen or a space.
- (\d{3})- the second capture group (-705-) e.g 0775-705-148
- [\s-]?- to match the space and the hyphen but its optional(?) since not all numbers are seperated by a hyphen or a space.
- (\d{3})- the third capture group (-148) e.g 0775-705-148

2. We also need to give each student a username that will be derived from their name as follows:
Yannis C Atieno will have a username ycatieno

`([A-Z])([a-z]+)\s([A-Z])\s([A-Za-z]+)(;\+254\d+)`

replace: `$1$2 $3 $4$5;\L$1\L$3\L$4`

- The \L is for the lowercase.
###### Solution:
- $1- ([A-Z])-The first initial of the first name(Y)from Yannisi
- $2- ([a-z]+)-The name (annisi) from the first name Yannisi
- \s- space after the first name.
- $3- ([A-Z])- The middle initial name (C) the range is in caps because the initial is in uppercase.
- \s- The space after the middle initial.
- $4- ([A-Za-z]+)- The last name (Atieno) the range is uppercase and lower case.
- $5- (;\+254\d+)- The phone number \+ to escape the + sign then the 254 then the \d+ for the rest of the digits.

### Repeat the #1 and #2 using sed tool

1. That is, add the prefix +254 and remove characters such as (, ), - or spaces.
`sed -E 's/[()-]//g; s/0?(254)?([0-9]{3})(\s?)([0-9]{3})(\s?)([0-9]{3})/+254\2\4\6/' regex.test.csv `
```
2956;Yannis C Atieno;+254775705148
2957;Yannis C Chacha;+254731485430
2958;Yannis C Idris;+254786408485
```
###### solution
- s/[()-]//g- to substitute the () and the - with nothing `/` we will add the `g` global to substitute their occurrences in the whole file.
- s/0?(254)?- to substitute numbers that start with 0 or 254 but its ? optional since not all numbers start with 0/254.
- ([0-9]{3})- our second capture group for the first three digits.
- (\s?)- third capture group for the numbers seperated by a space and its optional, since not all numbers are seperated by a space.
- ([0-9]{3})(\s?)([0-9]{3})- the forth ,fifth and sixth capture group. for the rest of the phone number.
- /+254\2\4\6/- substitute (/)it with +254 the second, forth and sixth capture group.(/)close the substitution then the file name regex.test.csv.

2. We also need to give each student a username that will be derived from their name as follows:
Yannis C Atieno will have a username ycatieno

`sed -E 's/^([0-9]+);([A-Z])([a-z]+) ([A-Z]) ([A-Za-z]+);(\+254[0-9]+)/\1;\2\3 \4 \5;\6;\L\2\4\5/' regex.test.csv `

2956;Yannis C Atieno;+254775705148;ycatieno
2957;Yannis C Chacha;+254731485430;ycchacha
###### solution
- /^([0-9]+);- substitute ^ start of line the school id (2956)followed by the ; separator.
- ([A-Z])- to capture the Y in Yannis.
- ([a-z]+)- to capture the annis in Yannis. Then followed by a space for the space separator.
- ([A-Z])- to capture the middle innitial(C) followed  by a space.
- ([A-Za-z]+);- to cature the last name (Atieno) followed by the; separator.
- (\+254[0-9]+)- to capture the phone number.
- /\1;\2\3 \4 \5;\6;\L\2\4\5/' regex.test.csv `- substitute it (/)with \1;\2\3 \4 \5;\6 then add the username at the end ;\L(for lowercase)\2\4\5.
## The vi / vim Editor
- vi and vim are editors that are Linux editors.

###### Using vi
Start vi Editor - start/open a vi editor session by simply typing vi pathToFile or vim pathToFile. vim is an improved version of vi.
vi has two(2) modes:
- Command mode - vi always starts in this mode. This mode allows you to:
-  Save
-  Copy lines (or text)
-  Paste text
-  Delete lines
-  Quit/exit from vi
- Insert mode - edit or type new text
### Commonly used vi commands
- Get into insert mode simply type i.
- Moving the cursor (Up, down, left, right arrows also work!):
  -  k - up one line
  -  j - down one line
  -  h - to the left one character position
  -  l - to the right one character position
- Invoke save, quit, move to given line commands be preceded by a colon : then hitting the enter/return key eg:
  -  :q - quits/exits vi
  -  :q! - quit and ignore any changes made
  -  :w - save
  -  :wq - save and quit
  -  :n - where n is any number so e.g. :36 will take the cursor to line #36 of the file if it exists.
- Copying, Pasting & deleting text:
  -  yy - copies the current line
  -  p - paste line(s) or text copied after the cursor.
  -  P - paste line(s) or text copied before the cursor.
  -  dd - deletes the line where the cursor is on.
  -  2yy - copies two(2) lines beginning with the one the cursor is on. Replace 2 with however many lines you wish to copy. Paste them all using p or P.
###### Task:
Test of vi knowledge (at the end of each step, save the file and exit vi):

1. Open the file created above an.other.conf.

`vim ~/Documents/vi-sandbox/.an.other.conf`

2. Edit server_name to read local.ann.other.

 `press i for insert. Edit local.an.other to local.ann.other`

3. Copy the line with access_log... and paste below the line with error_log
- navigate to the line with access_log and type `yy` to copy.
navigate to the line with error_log and type `p` to paste.

4. Navigate to line #19. Delete it.
- type `:19` to navigate to that line. Then type `dd` to delete.

###### Difference between vi and vim
-  They share the same core functionality, but vim has alot of additional features. vim(m-improved).
###### Displaying the total number of lines:
- press ctrl+g- to get the total number of lines.
- To get absolute line number- `:set number` and press enter.
- To turn them off, use `:set norelativenumber.`
##### Editing a file:
- i- Inserts text before the current cursor location
- I- Inserts text at the beginning of the current line
- a- Inserts text after the current cursor location
- A- Inserts text at the end of the current line
- o- Creates a new line for text entry below the cursor location
- O- Creates a new line for text entry above the cursor location
##### Deleting characters:
- x- Deletes the character under the cursor location
- X- Deletes the character before the cursor location
- dw- Deletes from the current cursor location to the next word
- d^- Deletes from the current cursor position to the beginning of the line
- d$- Deletes from the current cursor position to the end of the line
- D- Deletes from the cursor position to the end of the current line
- dd- Deletes the line the cursor is on
##### Change commands:
- cc- Removes the contents of the line, leaving you in insert mode.	
- cw- Changes the word the cursor is on from the cursor to the lowercase w end of the word.
- r- Replaces the character under the cursor. vi returns to the command mode after the replacement is entered.
- R- Overwrites multiple characters beginning with the character currently under the cursor. You must use Esc to stop the overwriting.
- s- Replaces the current character with the character you type. Afterward, you are left in the insert mode.
- S- Deletes the line the cursor is on and replaces it with the new text. After the new text is entered, vi remains in the insert mode.
##### Word and character searching:
- The / command searches forwards (downwards) in the file.

- The ? command searches backwards (upwards) in the file.
##### Replacing Text
The substitution command (:s/) enables you to quickly replace words or groups of words within your files.  Following is the syntax to replace text −

`:s/search/replace/g`

**Note**

1. You must be in command mode to use the commands. (Press Esc twice at any time to ensure that you are in command mode.)

2. You must be careful with the commands. These are case-sensitive.

3. You must be in insert mode to enter text.

## Section 3: Use sed or perl only for Advanced Text Manipulation

Please complete the Supplemental RegEx & vi - module before tackling this section. Avoid the -i flag unless you want the sed changes permanent. Some sed examples:
1. Display all students with ID starting with 11..:

`sed -n -E "s/(^11.*)/\1/gp" .test.student.csv`

Explanation:

- The **-n** flag will only display lines that get a match. All other output is suppressed
- The **-E**  flag allows you to use Extended RegEx syntax.
- The **s** char is stands for substitute.
- The first two **/** (forward slashes) contain the text (or text matching a pattern) to be substituted.
- The text in between the second **/** and the last one represents the replacement text.
- The **g** char after the last \ means the search and replace should be global ie all occurrences will be replaced. Omitting this will only relace the first occurrence.
- The **p** prints only lines with successful substitutions. 

2. For students with ID starting with 22.. display only their ID, name and email addresses:

`sed -n -E "s/(^22[0-9].*;)(.*;){4}(.*@.*)$/\1;\3/gp" .test.student.csv`

-  s/(^22[0-9].*;)- ^ start of line to match id starting with 22 [0-9]to match the rest of the number .* multiple occurrence.; the semicolon seperating the id and the first name.
-  (.*;){4}- matches any character(zero or multiple times followed by a semicolon). **{4}** matches that group 4times which will capture the: name, phone number, county number and the school number.
-  (.*@.*)$- matches the email and end of line$.
### Task
1. Print out all students with ID starting with 33...

`sed -n -E 's/(^33[0-9].*;)/\1/gp' .test.student.csv `
```
3300;Zora L Ratemo;0753-826-893;33;163;zlratemo@yahoo.com
3301;Zora L Wambugu;0781-450-247;44;174;zlwambugu@gmail.com
```
2. Find all students from county #22 (Ensure that students from school #22 are not accidentally included unless they are from county #22) and display their phone numbers without the hyphen eg.:

`sed -n -E 's/(^[0-9].*);([A-Za-z].*) ([A-Z]) ([A-Za-z].*);([0-9].*)(;22;)([0-9].*);(.*@.*)$/\1;\2 \3 \4;\5\6\7;\8/gp' .test.student.csv | tr -d '-'`
```
1086;Amber W Ratemo;0759920245;22;19;awratemo@email.com
1454;Edward C Kamau;0703605803;22;205;eckamau@hotmail.com
1479;Edward K Nuru;0757531359;22;46;eknuru@email.com
1568;Elizabeth K Mwangi;0729988948;22;7;ekmwangi@email.com
```
- The **tr command** is used to delete or substitute(translate) characters. eg
tr -d '-' deletes occurrences of hyphen(-).
example : tr '-' ' '- substitutes the hyphen with spaces. 

- You can also substitute the hyphens first:

 `sed -n -E 's/-//g; s/(^[0-9].*);([A-Za-z].*) ([A-Z]) ([A-Za-z].*);([0-9].*)(;22;)([0-9].*);(.*@.*)$/\1;\2 \3 \4;\5\6\7;\8/gp' .test.student.csv`
```
1086;Amber W Ratemo;0759920245;22;19;awratemo@email.com
1454;Edward C Kamau;0703605803;22;205;eckamau@hotmail.com
1479;Edward K Nuru;0757531359;22;46;eknuru@email.com
```
## Section 4: File Organization and Navigation

**1. Create four new directories inside .sampledata: A-F, G-L, M-R, and S-Z.**

 - To create a directory use the `mkdir` command.
 - Navigate to .sampledata: /Documents/git/quatrix-mentor/.sampledata.

   `mkdir A-F G-L M-R S-Z`

**2. Move all student data files (.txt) whose first name starts with A, B, C, D, E, or F into the A-F directory.**

- To list all student data files with first names A,B,C,D,E,F:

  `ls *_[A-F]*_*_*.txt`

- To move the files to A-F directory:

  `mv *_[A-F]*_*_*.txt A-F`

**3. Move all student data files (.txt) whose first name starts with G, H, I, J, K, or L into the G-L directory.**


   `mv *_[G-L]*_*_*.txt G-L`


**4. Move all student data files (.txt) whose first name starts with M, N, O, P, Q, or R into the M-R directory.**

   `mv *_[M-R]*_*_*.txt M-R`

**5. Move all remaining student data files (.txt) into the S-Z directory.**

    `mv *_[S-Z]*_*_*.txt S-Z`

**6. Navigate into the A-F directory using a relative path from your current location (the main directory where generate_data.sh is).**

   `cd A-F `

**7. From inside the A-F directory, list all files in the S-Z directory using a relative path.**

    `ls ../S-Z`

**8. From your current location (still inside A-F), restore all student data files (.txt) from all the categorized directories back into the main .sampledata directory.**
```
- To restore G-L: mv ../G-L/*.txt ..
- To restore M-R: mv ../M-R/*.txt ..
- To restore S-Z: mv ../S-Z/*.txt ..
- To restore A-F: since we are already in the A-F directory, we move all the .txt files to the .sample data which is the parent directory: mv *.txt ..
```
**9. Search/list for files for students where the last name starts with A and scored seventy-something ie 7X e.g.. 1273_Beth_K_Atieno.txt**

`find . -name "*_*_*_A*.txt" -exec grep -E ";7[0-9]+" {} +`
```
./2441_Mary_C_Atieno.txt:Swahili;70.6664
./2135_Joshua_P_Atieno.txt:English;76.6168
./2135_Joshua_P_Atieno.txt:Physics;79.3298
./1163_Ami_W_Atieno.txt:Agriculture;73.2947
```

**10. Search/list for files for students who have ...@gmail.com email addresses.**

 `find . -name "*.txt" -exec grep "@gmail.com" {} +`
 ```
./1778_Joan_P_Kamau.txt:Email: jpkamau@gmail.com
./2962_Okello_P_Yebo.txt:Email: opyebo@gmail.com
./2970_Okello_W_Maxx.txt:Email: owmaxx@gmail.com
./1039_Amber_L_Idris.txt:Email: alidris@gmail.com
```
**11. Undo the restructuring of the files ie move the files from e.g. A-F,...,S-Z back to where they were before started part (c) ie where all the files were in one folder. After you're done moving, delete the empty folders.**

`rmdir A-F G-L M-R S-Z`
- rm dir -deletes empty folders only. Cannot delete if it contains files.
- rm -r - removes recursively. Deletes files including all contents inside.

**12. Rename all files with Nate to be Nathan using: i) rename command and ii) using mv command and a bash loop of your choice and other commands you deem necessary.**

1) Using the rename command:
`rename 's/Nate/Nathan/' *.txt`

2) Using the mv command and a bash loop:
`for file in *Nate*.txt; do mv "$file" "${file/Nathan/Nate}"; done`

**13. Rename any occurrences of Nate to Nathan in all the *.txt files and in the .test.student.csv file as well**

1) To rename Nate to Nathan in .txt files:
`rename 's/Nate/Nathan' *.txt`

2) To rename Nate to Nathan inside the .txt files:
`sed -i 's/Nate/Nathan/g' *.txt`

3) To rename in the .test.student.csv:
`sed -i 's/Nate/Nathan/g' .test.student.csv`

**14. Remove any files for students with the name Joan (and be careful NOT to remove those for Joanne). Remove these lines in the csv file as well.**

- To list all files with Joan: 
ls *Joan*.txt - this will also include Joanne.

- To list only the Joan files : ls *Joan*.txt | grep -v "Joanne"

- To remove the Joan files :
`ls *Joan*.txt | grep -v "Joanne" | xargs rm`
-  grep -v prints everything except Joanne.

**15. Navigation:**

i) Navigate to the G-L folder that's inside the .sampledata folder with one command.
`cd .sampledata/G-L`

ii) Navigate to the root directory of the mentor repo with one command.
`cd ../../../../../../..` 

iii) Navigate to your home directory. Show at least two ways to do this.
`cd`
`cd ~`
`cd $HOME`

iv) From your home directory (ie WITHOUT navigating away from your home directory):
List the files in the .sampledata folder.
`ls Documents/git/quatrix-mentor/.sampledata`

v) List the folder and sub-folder and files structure/hierarchy of the mentor folder using just one command.
`tree Documents/git/quatrix-mentor/.sampledata`
ree Documents/git/quatrix-mentor
Documents/git/quatrix-mentor
Levels: tree -L 1
      : tree -L 2

## Section 5: Searching Data in .test.student.csv

**1. Display all lines from .test.student.csv where the phone number starts with 072.**

      `grep -E "; 072[0-9\-]*;" .test.student.csv`

- This will list phone numbers starting with 072
-  ; - Start after a semicolon (field boundary)
-  072 - Phone numbers beginning with 072
-  [0-9\-]* -	Followed by any combination of digits and dashes
-  ; - End of the field (next semicolon)

**2. Count how many students have an email address ending with @gmail.com in .test.student.csv.**

    `grep -E "@gmail\.com" .test.student.csv | wc -l`

-  grep -E "@gmail\.com" .test.student.csv -this will display students with this email address.
-  | wc -l - we will pipe the first command to (wc for word count). -l (counts only the number of lines).


**3. List the full names (second field) of all students from County ID 15 in .test.student.csv.**

- **awk** command is used for pattern scanning and processing language, useful for data extraction and reporting.
- Basic syntax:
  ***awk -F"<delimiter>" 'condition { action }' filename***

-  -F"<delimiter>"	-Tells awk what separates fields (e.g. ;, ,, or space)
-  condition	-Tells awk which lines to process (like a filter)
-  { action }	What to do when the condition is true (e.g., print something)
-  filename	-The input file to read

      ###### Solution:
    ` awk -F";" '$4==15 {print$2}' .test.student.csv `

- -F";" - tells awk that my csv file uses ; to seperate fields.
- $4==15 - the forth field is the countyid and we want to equate it to 15 because we want to search in county 15.
- {print $2}- we want to print the full names which is in the second field.


**4. Find the student ID, full name, and email address for any student whose name contains "Otieno" (case-insensitive) in .test.student.csv.**

    `awk -F";" '$2~/Otieno/ {print $1, $2, $6}' .test.student.csv `
- $2~/Otieno/ - the second field has three name so we cannot use the == to find any name otieno. This will match any line where the second field (full name) contains Otieno.
- {print $1, $2, $6} - this will print $1-the student id field, $2- the fullname field with the name Otieno, $6- the email address field.
-  The otput will be separated using spaces. But if i want to separate my output using ; i will add a **BEGIN {OFS=";"}**

   `awk -F";" 'BEGIN {OFS=";"}$2~/Otieno/ {print $1, $2, $6}' .test.student.csv`

-  BEGIN {OFS=";"} - output field separator makes awk use ; between the printed fields.

**5. Display the phone numbers of all students who attend School ID 50 in .test.student.csv.**

    `awk -F";" '$5==50 {print $3}' .test.student.csv`
-  The school id is the fifth field so we will set the variable5 to be equals to 50 then we print the third field which is the phone numbers.

**6. Count the total number of students listed in .test.student.csv (excluding any header if it existed, but your script doesn't generate one).**

    `awk -F";" '{print $2}' .test.student.csv | wc -l`
-  The students name is the second field so will print that then count how many lines.

**7. Find all unique domain names used in student email addresses from .test.student.csv.**

    `awk -F";" '{print $6}' .test.student.csv | cut -d"@" -f2 | sort | uniq`

##### Solution:
-  awk -F";" '{print $6}' .test.student.csv - this will print the sixth field for the email addresses.
-  cut -d"@" -f2- since we want the domain names , this will split the email address at the **@** symbol, then pick the second field **-f2** for the domain names.
-  sort - this sorts all the domain names alphabetically.
-  uniq- this removes all the duplicates. e.g email.com
```
gmail.com
hotmail.com
yahoo.com
```
-  To count how many times each domain appears: **uniq -c**
``` 
    542 email.com
    529 gmail.com
    617 hotmail.com
    562 yahoo.com
```

## Section 6: Automation with Bash Scripting

**Bash script**- a text file containing a series of commands you could normally type in your terminal instead of runnimg commands one by one, you put them in a script.

**1. Create a Bash script named organize_students.zsh that performs the file organization task from Section 3 (creating the A-F, G-L, M-R, S-Z directories and moving files into them). Make sure it's executable.**
-   To create a bash script:
```touch organize_students.zsh```
- To edit the file :
```vi organize_students.zsh```

```
#!/bin/bash

# create folders
mkdir A-F G-L M-R S-Z
# To move the files.
mv *_[A-F]*_*_*.txt A-F
mv *_[G-L]*_*_*.txt G-L
mv *_[M-R]*_*_*.txt M-R
mv *_[S-Z]*_*_*.txt S-Z
```

- To make the file executable: 

```chmod u+x organize_students.zsh```

**2. Create a Bash script named find_072_phones.zsh that searches .test.student.csv for all phone numbers starting with 072 and outputs only those phone numbers to the terminal. Make it executable.**

**touch find_072_phones.zsh**

**vi find_072_phones.zsh**
```
#!/bin/bash
# phone numbers starting with 072
awk -F";" '$3~/^072/{print $3}' .test.student.csv
```


**3. Create a Bash script named county_student_count.zsh that takes a county ID as its first argument and outputs the number of students from that county in .test.student.csv.**

```
#!/bin/bash
county_id="$1"
awk -F";" '$4== '"$county_id" ' '.test.student.csv | wc -l
```

**4. Example usage: ./county_student_count.zsh 10**
- To run the script:
`./county_student_count.zsh 10`

**5. Create a Bash script named restore_data.zsh that moves all student data files (.txt) from the categorized directories (A-F, G-L, etc.) back into the main .sampledata directory and then removes the empty categorized directories. Make it executable.**
```
#!/bin/bash

#move files back
mv ~/Documents/git/quatrix-mentor/.sampledata/A-F/*.txt ~/Documents/git/quatrix-mentor/.sampledata
mv ~/Documents/git/quatrix-mentor/.sampledata/G-L/*.txt ~/Documents/git/quatrix-mentor/.sampledata
mv ~/Documents/git/quatrix-mentor/.sampledata/M-R/*.txt ~/Documents/git/quatrix-mentor/.sampledata
mv ~/Documents/git/quatrix-mentor/.sampledata/S-Z/*.txt ~/Documents/git/quatrix-mentor/.sampledata
```
- To remove the empty directories add:
`rmdir A-F G-L M-R S-Z`

**6. Create a Bash script named full_cleanup.zsh that runs the cleanup function from generate_data.sh and then also removes all .test.*.csv files. Make it executable.**

```
#!/bin/bash

# source the generate_data.sh
./util/generate_exam_data.sh

# remove .test.*.csv
rm .test.*.csv
```
- If you run this it will restore back the .test.*.csv files:
```
./util/generate_exam_data.sh 
Generating Exam data. Please wait... 100%
Populating Exam database. Please wait... 1%psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  role "lwachira" does not exist
Populating Exam database. Please wait... 100%
Exam data generation and database population completed successfully.
(see .generate_exam_data.log for details)
```
