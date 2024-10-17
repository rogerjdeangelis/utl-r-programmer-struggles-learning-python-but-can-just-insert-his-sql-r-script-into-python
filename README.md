# utl-r-programmer-struggles-learning-python-but-can-just-insert-his-sql-r-script-into-python
R programmer struggles learning python but can just insert his sql r script into python
    %let pgm=utl-r-programmer-struggles-learning-python-but-can-just-insert-his-sql-r-script-into-python;

    %stop_submission;

    R programmer struggles learning python but can just insert his sql r script into python

         SOLUTIONS
             1 sas sql
             2 r sql
             3 python sql
             4 does not work? (also requires knowledge of the panda language)
               I could not get the posted solution to work (see below)
               the variable day does not appear in the solution?

    stackoverflow python
    https://tinyurl.com/zvfkpnem
    https://stackoverflow.com/questions/79099006/adding-custom-arithmetic-aggregation-in-a-grouped-dataframe-along-with-agg-func

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                             |                                                          |                               */
    /*            INPUT            | PROCESS(SELEXPLANATORY SQL SAME CODE SAS R PYTHON)       |          OUTPUT               */
    /*            ====             | ==================================================       |          ======               */
    /*                             |                                                          |                               */
    /*        FISCAL_              | SELF EXPLANATORY SQL                                     |       FISCAL_  SALES_  SALES_ */
    /* NAME    YEAR     DAY  SALE  | select                                                   | NAME   YEAR      SUM     AVG  */
    /*                             |    name                                                  |                               */
    /*  a    FY2023-24   1    100  |   ,fiscal_year                                           |  a   FY2023-24   633    316.5 */
    /*  a    FY2023-24   2    222  |   ,sum(sale) as sales_sum                                |  a   FY2024-25  1698    849.0 */
    /*  a    FY2024-25   1    333  |   ,sum(sale)/count(distinct(day)) as sales_avg           |  b   FY2023-24  3095   1547.5 */
    /*  a    FY2024-25   2    444  | from                                                     |  b   FY2024-25  1462    731.0 */
    /*  a    FY2023-24   1    200  |    have                                                  |                               */
    /*  a    FY2023-24   2    111  | group                                                    |                               */
    /*  a    FY2024-25   1    555  |    by name, fiscal_year                                  |                               */
    /*  a    FY2024-25   2    366  |                                                          |                               */
    /*  b    FY2023-24   1    666  |                                                          |                               */
    /*  b    FY2023-24   2    777  | DATA SORTED FOR DOCUMENTATION PURPOSES                   |                               */
    /*  b    FY2024-25   1    300  | SOLUTIONS DOE NOT REQUIRE THE SORT                       |                               */
    /*  b    FY2024-25   2    345  |                                                          |                               */
    /*  b    FY2023-24   1    756  |        FISCAL_              SUM   SUM SALE               |                               */
    /*  b    FY2023-24   2    896  | NAME    YEAR     DAY  SALE  SALE  /CNT DISTINCT DAYS     |                               */
    /*  b    FY2024-25   1    452  |                                                          |                               */
    /*  b    FY2024-25   2    365  |  a    FY2023-24   1    100                               |                               */
    /*                             |  a    FY2023-24   2    222                               |                               */
    /*                             |  a    FY2023-24   1    200                               |                               */
    /*                             |  a    FY2023-24   2    111  633   633/2 (distinct days)  |                               */
    /*                             |                                   316.5                  |                               */
    /*                             |  a    FY2024-25   1    333                               |                               */
    /*                             |  a    FY2024-25   2    444                               |                               */
    /*                             |  a    FY2024-25   1    555                               |                               */
    /*                             |  a    FY2024-25   2    366 1698   1698/2 (distinct days) |                               */
    /*                             |                                    849                   |                               */
    /*                             |                                                          |                               */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
       retain name fiscal_year day sale;
       input Name$  day Fiscal_Year $10.  sale;
    cards4;
    a 1 FY2023-24 100
    a 2 FY2023-24 222
    a 1 FY2024-25 333
    a 2 FY2024-25 444
    a 1 FY2023-24 200
    a 2 FY2023-24 111
    a 1 FY2024-25 555
    a 2 FY2024-25 366
    b 1 FY2023-24 666
    b 2 FY2023-24 777
    b 1 FY2024-25 300
    b 2 FY2024-25 345
    b 1 FY2023-24 756
    b 2 FY2023-24 896
    b 1 FY2024-25 452
    b 2 FY2024-25 365
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*           FISCAL_                                                                                                      */
    /*  NAME      YEAR       DAY    SALE                                                                                      */
    /*                                                                                                                        */
    /*   a      FY2023-24     1      100                                                                                      */
    /*   a      FY2023-24     2      222                                                                                      */
    /*   a      FY2024-25     1      333                                                                                      */
    /*   a      FY2024-25     2      444                                                                                      */
    /*   a      FY2023-24     1      200                                                                                      */
    /*   a      FY2023-24     2      111                                                                                      */
    /*   a      FY2024-25     1      555                                                                                      */
    /*   a      FY2024-25     2      366                                                                                      */
    /*   b      FY2023-24     1      666                                                                                      */
    /*   b      FY2023-24     2      777                                                                                      */
    /*   b      FY2024-25     1      300                                                                                      */
    /*   b      FY2024-25     2      345                                                                                      */
    /*   b      FY2023-24     1      756                                                                                      */
    /*   b      FY2023-24     2      896                                                                                      */
    /*   b      FY2024-25     1      452                                                                                      */
    /*   b      FY2024-25     2      365                                                                                      */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */

    proc sql;
      create
         table want as
      select
         name
        ,fiscal_year
        ,sum(sale) as sales_sum
        ,sum(sale)/count(distinct(day)) as sales_avg
      from
         sd1.have
      group
         by name, fiscal_year
    ;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*            FISCAL_     SALES_    SALES_                                                                                */
    /*   NAME      YEAR         SUM       AVG                                                                                 */
    /*                                                                                                                        */
    /*    a      FY2023-24      633      316.5                                                                                */
    /*    a      FY2024-25     1698      849.0                                                                                */
    /*    b      FY2023-24     3095     1547.5                                                                                */
    /*    b      FY2024-25     1462      731.0                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(sqldf)
    library(haven)
    source("c:/oto/fn_tosas9x.r")
    have<-read_sas("d:/sd1/have.sas7bdat")
    have;
    want <- sqldf('
      select
         name
        ,fiscal_year
        ,sum(sale) as sales_sum
        ,sum(sale)/count(distinct(day)) as sales_avg
      from
         have
      group
         by name, fiscal_year
      ')
    want;
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rwant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* R                                        SAS                                                                           */
    /* > want;                                                                                                                */
    /*                                                               FISCAL_     SALES_    SALES_                             */
    /*   NAME FISCAL_YEAR sales_sum sales_avg   ROWNAMES    NAME      YEAR         SUM       AVG                              */
    /*                                                                                                                        */
    /* 1    a   FY2023-24       633     316.5       1        a      FY2023-24      633      316.5                             */
    /* 2    a   FY2024-25      1698     849.0       2        a      FY2024-25     1698      849.0                             */
    /* 3    b   FY2023-24      3095    1547.5       3        b      FY2023-24     3095     1547.5                             */
    /* 4    b   FY2024-25      1462     731.0       4        b      FY2024-25     1462      731.0                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql('''
      select
         name
        ,fiscal_year
        ,sum(sale) as sales_sum
        ,sum(sale)/count(distinct(day)) as sales_avg
      from
         have
      group
         by name, fiscal_year
       ''');
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* PYTHON                                      SAS                                                                        */
    /*                                                      FISCAL_     SALES_    SALES_                                      */
    /*    NAME FISCAL_YEAR  sales_sum  sales_avg   NAME      YEAR         SUM       AVG                                       */
    /*                                                                                                                        */
    /*  0    a   FY2023-24      633.0      316.5    a      FY2023-24      633      316.5                                      */
    /*  1    a   FY2024-25     1698.0      849.0    a      FY2024-25     1698      849.0                                      */
    /*  2    b   FY2023-24     3095.0     1547.5    b      FY2023-24     3095     1547.5                                      */
    /*  3    b   FY2024-25     1462.0      731.0    b      FY2024-25     1462      731.0                                      */
    /*                                                                                                                        */
    /**************************************************************************************************************************/ */

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

