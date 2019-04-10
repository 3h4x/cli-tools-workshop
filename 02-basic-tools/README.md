## Useful commands

Every command used in this part of workshop will utilize `countries.csv` file. It contains list of countires with some additional data in `csv` format delimited by `,`
 
## head and tail 

`head` is used to get just n-th number of rows starting from start of a file. Flag `-n` defines how many rows we want to get (default is 10).

`head -n1 countries.csv`  
Output: `name,alpha-2,alpha-3,country-code,iso_3166-2,region,sub-region,intermediate-region,region-code,sub-region-code,intermediate-region-code`

`tail` is same as `head` but it starts from end of the file.  
`tail -n1 countries.csv`  
Output: `Zimbabwe,ZW,ZWE,716,ISO 3166-2:ZW,Africa,Sub-Saharan Africa,Eastern Africa,002,202,014`
 
## cat

`cat` is command used to get content of a file

`cat countries.csv`  
Output: will print in terminal whole file

## wc
 
## grep

`grep` comes from `ed` command `g/re/p` which will globally search for regular expression.  
Most commonly `grep` is used to search for string in files and print matching lines.

`grep Greenland countries.csv`  
This will print every line that contains line with `Greenland` word in file.

`grep -n Greenland countries.csv` will print number of matched line  
`grep -A 2 Greenland countries.csv` print 2 lines after match  
`grep -B 5 Greenland countries.csv` print 3 lines before match   

## cut

`cut` is used to trim string.  
You can use flag `-d` which will tell `cut` command what is the delimiter that you want to use and `-f` for delimited field that you want to get.   

Let's take just third field of this csv which is country code.  
`grep -n Greenland countries.csv | cut -f 3 -d,`  
Output: `GRL`


Let's take just fields from 9th till end of this csv.  
`grep -n Greenland countries.csv | cut -f 9- -d,`  
Output: `019,021,""`
 
## sort

## uniq
