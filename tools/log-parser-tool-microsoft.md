# Log Parser Tool from Microsoft

This command line tool is a bit of a swiss army knife.  

Find it here:

[Microsoft Log Parser tool](https://www.microsoft.com/en-us/download/confirmation.aspx?id=24659)

## Prep

You'll have to add the install path to your [PATH variable](https://www.java.com/en/download/help/path.xml) to make it useful:

```
C:\Program Files (x86)\Log Parser 2.2
```
## Sample Query

```
logparser "SELECT TOP 10 * from flightlist_20200101_20200131.csv"
```

Results in:

![Screenshot](/img/2020.04.24.10.44.0000.jpg "Screenshot")

## Help file 

```
Usage:   LogParser [-i:<input_format>] [-o:<output_format>] <SQL query> |
                   file:<query_filename>[?param1=value1+...]
                   [<input_format_options>] [<output_format_options>]
                   [-q[:ON|OFF]] [-e:<max_errors>] [-iw[:ON|OFF]]
                   [-stats[:ON|OFF]] [-saveDefaults] [-queryInfo]

         LogParser -c -i:<input_format> -o:<output_format> <from_entity>
                   <into_entity> [<where_clause>] [<input_format_options>]
                   [<output_format_options>] [-multiSite[:ON|OFF]]
                   [-q[:ON|OFF]] [-e:<max_errors>] [-iw[:ON|OFF]]
                   [-stats[:ON|OFF]] [-queryInfo]

 -i:<input_format>   :  one of IISW3C, NCSA, IIS, IISODBC, BIN, IISMSID,
                        HTTPERR, URLSCAN, CSV, TSV, W3C, XML, EVT, ETW,
                        NETMON, REG, ADS, TEXTLINE, TEXTWORD, FS, COM (if
                        omitted, will guess from the FROM clause)
 -o:<output_format>  :  one of CSV, TSV, XML, DATAGRID, CHART, SYSLOG,
                        NEUROVIEW, NAT, W3C, IIS, SQL, TPL, NULL (if omitted,
                        will guess from the INTO clause)
 -q[:ON|OFF]         :  quiet mode; default is OFF
 -e:<max_errors>     :  max # of parse errors before aborting; default is -1
                        (ignore all)
 -iw[:ON|OFF]        :  ignore warnings; default is OFF
 -stats[:ON|OFF]     :  display statistics after executing query; default is
                        ON
 -c                  :  use built-in conversion query
 -multiSite[:ON|OFF] :  send BIN conversion output to multiple files
                        depending on the SiteID value; default is OFF
 -saveDefaults       :  save specified options as default values
 -restoreDefaults    :  restore factory defaults
 -queryInfo          :  display query processing information (does not
                        execute the query)
```						

## Query Language
It uses a variant of SQL:

```
SQL Language Grammar-------------------------------------------------------------------------------
<query>               -> <select_clause> [ <using_clause>] [ <into_clause> ]
                         <from_clause> [ <where_clause> ] [ <group_by_clause> ]
                         [ <having_clause> ] [ <order_by_clause> ]
<select_clause>       -> SELECT [ TOP <integer> ] [ DISTINCT | ALL ]
                           <selection_list>
<selection_list>      -> <selection_list_el> [ , <selection_list> ]
<selection_list_el>   -> <field_expr> [ AS <alias> ] |
                         *
<using_clause>        -> USING <selection_list>
<into_clause>         -> INTO <into_entity>
<from_clause>         -> FROM <from_entity>
<where_clause>        -> WHERE <expression>
<expression>          -> <term1> [ OR <expression> ]
<term1>               -> <term2> [ AND <term1> ]
<term2>               -> <field_expr> <rel_op> <field_expr>                 |
                         <field_expr> [ NOT ] LIKE <like_value>             |
                         <field_expr> [ NOT ] BETWEEN <field_expr> AND
                              <field_expr>                                  |
                         <field_expr> <unary_op>                            |
                         <field_expr> <incl_op> <content>                   |
                         <field_expr> <rel_op> [ALL|ANY] <content>          |
                         ( <field_expr_list> ) <incl_op> <content>          |
                         ( <field_expr_list> ) <rel_op> [ALL|ANY] <content> |
                         NOT <term2>                                        |
                         ( <expression> )
<content>             -> ( <value_list> ) |
                         ( <query> )

<group_by_clause>     -> GROUP BY <field_expr_list> [ WITH ROLLUP ]

<having_clause>       -> HAVING <expression>

<order_by_clause>     -> ORDER BY <field_expr_list> [ ASC | DESC ] |
                         ORDER BY * [ ASC | DESC ]

<field_expr_list>     -> <field_expr> [ , <field_expr_list> ]
<field_expr>          -> <sqlfunction_expr>     |
                         <function_expr>        |
                         <value>                |
                         <alias>                |
                         <field>
<sqlfunction_expr>    -> <sqlfunction> ( [ DISTINCT | ALL ] <field_expr> )   |
                         <prop_sqlfunction> ( <field_expr> ) [ <on_fields> ] |
                         COUNT ( [ DISTINCT | ALL ] * )                      |
                         COUNT ( [ DISTINCT | ALL ] <field_expr_list> )      |
                         PROPCOUNT ( * ) [ <on_fields> ]                     |
                         PROPCOUNT ( <field_expr_list> ) [ <on_fields> ]
<function_expr>       -> <function> ( <field_expr_list> ) |
                         <case_statement>
<value_list>          -> <value_list_row> [ ; <value_list> ]
<value_list_row>      -> <value> [ , <value_list_row> ]
<sqlfunction>         -> SUM | AVG | MAX | MIN | GROUPING
<prop_sqlfunction>    -> PROPSUM
<on_fields>           -> ON ( <field_expr_list> )
<function>            -> ADD | BIT_AND | BIT_NOT | BIT_OR | BIT_SHL          |
                         BIT_SHR | BIT_XOR | COALESCE | COMPUTER_NAME | DIV  |
                         EXP | EXP10 | EXTRACT_EXTENSION | EXTRACT_FILENAME  |
                         EXTRACT_PATH | EXTRACT_PREFIX | EXTRACT_SUFFIX      |
                         EXTRACT_TOKEN | EXTRACT_VALUE | FLOOR               |
                         HASHMD5_FILE | HASHSEQ | HEX_TO_ASC | HEX_TO_HEX16  |
                         HEX_TO_HEX32 | HEX_TO_HEX8 | HEX_TO_INT             |
                         HEX_TO_PRINT | IN_ROW_NUMBER | INDEX_OF             |
                         INT_TO_IPV4 | IPV4_TO_INT | LAST_INDEX_OF | LOG     |
                         LOG10 | LTRIM | MOD | MUL | OUT_ROW_NUMBER          |
                         QNTFLOOR_TO_DIGIT | QNTROUND_TO_DIGIT | QUANTIZE    |
                         REPLACE_CHR | REPLACE_IF_NOT_NULL | REPLACE_STR     |
                         RESOLVE_SID | REVERSEDNS | ROT13 | ROUND | RTRIM    |
                         SEQUENCE | SQR | SQRROOT | STRCAT | STRCNT | STRLEN |
                         STRREPEAT | STRREV | SUB | SUBSTR | SYSTEM_DATE     |
                         SYSTEM_TIME | SYSTEM_TIMESTAMP | SYSTEM_UTCOFFSET   |
                         TO_DATE | TO_HEX | TO_INT | TO_LOCALTIME            |
                         TO_LOWERCASE | TO_REAL | TO_STRING | TO_TIME        |
                         TO_TIMESTAMP | TO_UPPERCASE | TO_UTCTIME | TRIM     |
                         URLESCAPE | URLUNESCAPE | WIN32_ERROR_DESCRIPTION
<case_statement>      -> CASE <field_expression> <when_statement_list>
                           [ <else_statement> ] END
<when_statement_list> -> <when_statement> [ , <when_statement_list> ]
<when_statement>      -> WHEN <field_expression> THEN <field_expression>
<else_statement>      -> ELSE <field_expression>
<value>               -> <string_value> |
                         <real>         |
                         <integer>      |
                         <timestamp>    |
                         NULL
<rel_op>              -> < | > | <> | = | <= | >=
<incl_op>             -> IN | NOT IN
<unary_op>            -> IS NULL | IS NOT NULL
<timestamp>           -> TIMESTAMP ( <string_value> , <timestamp_format> )
<timestamp_format>    -> ' *( <timestamp_separator> ) *( <timestamp_element>
                           *( <timestamp_separator> ) )'
<timestamp_element>   -> 1*4 y        |
                         1*4 M        |
                         MX | MP      |
                         1*4 d        |
                         dx | dp      |
                         1*2 h        |
                         hx | hp      |
                         1*2 m        |
                         mx | mp      |
                         1*2 s        |
                         sx | sp      |
                         1*2 l        |
                         lx | lp      |
                         1*2 n        |
                         nx | np      |
                         tt
<timestamp_separator> -> <any_char_except_timestamp_element> |
                         '?'
<field>              -> '[' <field_name> ']'    |
                         <field_name>
<like_value>          -> ' *( <any_char> | % | _ ) '
<string_value>        -> ' *( <any_char> ) '
<comment>             -> '/*' <text> '*/'    |
                         '//' <text> CRLF
```
