
# Finds the right CSV separator and excludes bad lines
### pip install outguncsv
#### Example:
```python

# You have probably seen this before, right?
import pandas as pd
pd.read_csv(r"https://github.com/zdavatz/diprela/raw/main/csv/diprela.csv")
Traceback (most recent call last):
  File "C:\Users\Gamer\anaconda3\envs\dfdir\lib\site-packages\IPython\core\interactiveshell.py", line 3398, in run_code
    exec(code_obj, self.user_global_ns, self.user_ns)
  File "<ipython-input-8-c5703c9ae399>", line 1, in <cell line: 1>
  ....
    File "pandas\_libs\parsers.pyx", line 1973, in pandas._libs.parsers.raise_parser_error
pandas.errors.ParserError: Error tokenizing data. C error: Expected 1 fields in line 3, saw 10



pd.read_csv(r"https://github.com/zdavatz/diprela/raw/main/csv/diprela.csv",on_bad_lines='skip')
# Better, but everything in one column, and we have lost about 600 rows. 
    Schweizerische Nährwertdatenbank komplett (bearbeitet durch Lesley Grünenfelder) (Stand: 11.02.2023) ;;;;;;;;;;;;;;;;;;;;;;;;;;;Schweizerische Nährwertdatenbank komplett (bearbeitet durch Lesley Grünenfelder) (Stand: 30.01.2023) ;;;;;;;;;;;;;;;;;;;;;
0     ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;                                                                                                                                                                                                        
1    Agar Agar;;Gelier- und Bindemittel ;Verschiede...                                                                                                                                                                                                        
2    Agavensirup;Agavendicksaft ;Zucker und Süsssto...                                                                                                                                                                                                        
3    Ahornsirup;;Zucker und Süssstoffe;Verschiedene...                                                                                                                                                                                                        
4    Älplermagronen;zubereitet;salzige Gerichte ;Ge...                                                                                                                                                                                                        
..                                                 ...                                                                                                                                                                                                        
521  Zwieback ;;Brot und Backware ;Getreide und Get...                                                                                                                                                                                                        
522  Zwieback;Vollkorn;Brot und Backware ;Getreide ...                                                                                                                                                                                                        
523  Zwiebel;gedünstet (ohne Zugabe von Fett und Sa...                                                                                                                                                                                                        
524  Zwiebel;geröstet (ohne Zugabe von Fett und Sal...                                                                                                                                                                                                        
525  Zwiebel;roh;Gemüse frisch ;Gemüse ;pro 100g es...                                                                                                                                                                                                        
[526 rows x 1 columns]



# If you have problems reading a CSV file, use: 
from outguncsv import read_balky_csv_files
alf3 = r"https://github.com/zdavatz/diprela/raw/main/csv/diprela.csv"
df3 = read_balky_csv_files(
    csvfiles=alf3,
    encoding="utf-8",
    sep=None,
    regexremove=(),
    filepathcolumn="file",
    on_bad_lines="warn",
)


df3
Out[4]: 
                                                      0  ...                                               file
0     Schweizerische Nährwertdatenbank komplett (bea...  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1                                                   NaN  ...  https://github.com/zdavatz/diprela/raw/main/cs...
2                                                  Name  ...  https://github.com/zdavatz/diprela/raw/main/cs...
3                                             Agar Agar  ...  https://github.com/zdavatz/diprela/raw/main/cs...
4                                           Agavensirup  ...  https://github.com/zdavatz/diprela/raw/main/cs...
                                                 ...  ...                                                ...
1213                                            Zwiebel  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1214                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1215                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1216                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1217                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
[1218 rows x 50 columns]


```

```python
from outguncsv import read_balky_csv_files
import glob
alf = glob.glob(
    r"C:\Users\Gamer\Documents\Downloads\anyascii-master\input\tables\*.tsv"
)
df = read_balky_csv_files(
    csvfiles=alf,  # list or string (url/file path)
    encoding="utf-8",
    sep=None,  # if None, it does its best to find the best separator
    regexremove=(),  # remove lines, regex must be in binary: rb"^\s*#\s+.*$",
    filepathcolumn="file",  # a new colum will be created with the file path
    on_bad_lines="skip",  # use either skip or warn, it won't work with error
    # for *args, **kwargs -> https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html
	
	
)

alf = r"https://raw.githubusercontent.com/pandas-dev/pandas/main/doc/data/titanic.csv"
df2 = read_balky_csv_files(
    csvfiles=alf,
    encoding="utf-8",
    sep=None,
    regexremove=(),
    filepathcolumn="file",
    on_bad_lines="skip",
)
alf3 = r"https://github.com/zdavatz/diprela/raw/main/csv/diprela.csv"
df3 = read_balky_csv_files(
    csvfiles=alf3,
    encoding="utf-8",
    sep=None,
    regexremove=(),
    filepathcolumn="file",
    on_bad_lines="warn",
)
alf4 = "https://github.com/curran/data/raw/gh-pages/migrants/events.csv"
df4 = read_balky_csv_files(
    csvfiles=alf4,
    encoding="utf-8",
    sep=",",
    regexremove=(),
    filepathcolumn="file",
    on_bad_lines="skip",
)


df
Out[3]: 
       0  1                                               file
0      𞤢  a  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
1      𞤣  d  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
2      𞤤  l  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
3      𞤥  m  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
4      𞤦  b  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
   .. ..                                                ...
14439  𜾿  -  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
14440  𜿀  -  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
14441  𜿁  -  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
14442  𜿂  -  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
14443  𜿃  -  C:\Users\Gamer\Documents\Downloads\anyascii-ma...
[14444 rows x 3 columns]
df2
Out[4]: 
       0  1  2  ...    10 11                                               file
0      1  0  3  ...   NaN  S  https://raw.githubusercontent.com/pandas-dev/p...
1      2  1  1  ...   C85  C  https://raw.githubusercontent.com/pandas-dev/p...
2      3  1  3  ...   NaN  S  https://raw.githubusercontent.com/pandas-dev/p...
3      4  1  1  ...  C123  S  https://raw.githubusercontent.com/pandas-dev/p...
4      5  0  3  ...   NaN  S  https://raw.githubusercontent.com/pandas-dev/p...
..   ... .. ..  ...   ... ..                                                ...
886  887  0  2  ...   NaN  S  https://raw.githubusercontent.com/pandas-dev/p...
887  888  1  1  ...   B42  S  https://raw.githubusercontent.com/pandas-dev/p...
888  889  0  3  ...   NaN  S  https://raw.githubusercontent.com/pandas-dev/p...
889  890  1  1  ...  C148  C  https://raw.githubusercontent.com/pandas-dev/p...
890  891  0  3  ...   NaN  Q  https://raw.githubusercontent.com/pandas-dev/p...
[891 rows x 13 columns]
df3
Out[5]: 
                                                      0  ...                                               file
0     Schweizerische Nährwertdatenbank komplett (bea...  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1                                                   NaN  ...  https://github.com/zdavatz/diprela/raw/main/cs...
2                                                  Name  ...  https://github.com/zdavatz/diprela/raw/main/cs...
3                                             Agar Agar  ...  https://github.com/zdavatz/diprela/raw/main/cs...
4                                           Agavensirup  ...  https://github.com/zdavatz/diprela/raw/main/cs...
                                                 ...  ...                                                ...
1213                                            Zwiebel  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1214                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1215                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1216                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
1217                                      Zwiebelkuchen  ...  https://github.com/zdavatz/diprela/raw/main/cs...
[1218 rows x 50 columns]
df4
Out[6]: 
           0  ...                                               file
0        NaN  ...  https://github.com/curran/data/raw/gh-pages/mi...
1    57234.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
2    56633.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
3    72740.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
4    55194.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
..       ...  ...                                                ...
955  36496.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
956  36500.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
957  36499.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
958  36503.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
959  36502.0  ...  https://github.com/curran/data/raw/gh-pages/mi...
[960 rows x 22 columns]
```
