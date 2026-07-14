# rapidminer-slc-calling-postgresql-creating-summarizing-database-tables-no-gui
RapidMiner slc calling postgresql creating summarizing database tables-no-gui
    %let pgm=rapidminer-slc-calling-postgresql-creating-summarizing-database-tables-no-gui ;

    %stop_submission;

    RapidMiner slc calling postgresql creating summarizing database tables-no-gui;

    Too long to post here, see
    https://github.com/rogerjdeangelis/rapidminer-slc-calling-postgresql-creating-summarizing-database-tables-no-gui

    EXAMPLES

       1 SLC LANGUAGE            : SELECT THE FOUR YOUNGEST STUDENTS BY SEX IN MATH CLASS
       2 PASSTHRU POSTGRESSQL SQL: SELECT THE FOUR YOUNGEST STUDENTS BY SEX IN MATH CLASS

    CONTENTS

       1 Install postgresql for win 11 64bit (without the need for a password)
       2 Create postgreSQL table
       3 Base SLC language select 4 youngest by sex
       4 Passthru Postgresql sql select 4 youngest by sex

    /*   _           _        _ _                   _                            _
    / | (_)_ __  ___| |_ __ _| | |  _ __   ___  ___| |_ __ _ _ __ ___  ___  __ _| |
    | | | | `_ \/ __| __/ _` | | | | `_ \ / _ \/ __| __/ _` | `__/ _ \/ __|/ _` | |
    | | | | | | \__ \ || (_| | | | | |_) | (_) \__ \ || (_| | | |  __/\__ \ (_| | |
    |_| |_|_| |_|___/\__\__,_|_|_| | .__/ \___/|___/\__\__, |_|  \___||___/\__, |_|
                                   |_|                 |___/                  |_|
     INSTALL POSTGRESQL FOR WIN 11 64BIT
    */

     a  https://www.enterprisedb.com/downloads/postgres-postgresql-downloads

     b  Turn passwords  off

        Go to
        C:\Program Files\PostgreSQL\18\data\pg_hba,conf

        edit
        ip4 and ip6 replace scram-sha-256 with trust

        # IPv4 local connections:
        host    all             all   127.0.0.1/32   trust
        # IPv6 local connections:
        host    all             all   ::1/128        trust

        open command window and restart postgresql-x64-18 service

        net stop postgresql-x64-18
        net start postgresql-x64-18

     c Use builtin database 'template1'

     c Use builtin superuser name 'postgres'

     d Connection methods

       LIBNAME mydb POSTGRESQL
         USER='postgres'
         SERVER='localhost'
         DATABASE='template1'
         PRESERVE_TAB_NAMES=YES;
         ..
       LIBNAME mydb clear;

       proc sql;
         connect to postgresql (
            USER='postgres'
            SERVER='localhost'
            DATABASE='template1'
            PRESERVE_TAB_NAMES=YES
            );
            ..
         disconnect from postgresql;
       quit;

    /*___                        _                        _                            _   _        _     _
    |___ \    ___ _ __ ___  __ _| |_ ___  _ __   ___  ___| |_ __ _ _ __ ___  ___  __ _| | | |_ __ _| |__ | | ___
      __) |  / __| `__/ _ \/ _` | __/ _ \| `_ \ / _ \/ __| __/ _` | `__/ _ \/ __|/ _` | | | __/ _` | `_ \| |/ _ \
     / __/  | (__| | |  __/ (_| | ||  __/| |_) | (_) \__ \ || (_| | | |  __/\__ \ (_| | | | || (_| | |_) | |  __/
    |_____|  \___|_|  \___|\__,_|\__\___|| .__/ \___/|___/\__\__, |_|  \___||___/\__, |_|  \__\__,_|_.__/|_|\___|
                                         |_|                 |___/                  |_|
    Using base rapidminer sslc lagguage ri sekect 4 youngest math class students by sex
    */

    LIBNAME mydb POSTGRESQL
      USER='postgres'
      SERVER='localhost'
      DATABASE='template1'
      PRESERVE_TAB_NAMES=YES;

    proc datasets lib=mydb kill;
    run;quit;

    data mydb.math;
    informat
       name $8.
       sex $1.
       age 8.
       height 8.
       weight 8.
       ;
    input
      name sex age height weight;
    cards4;
    Alfred M 14 69 112.5
    Alice F 13 56.5 84
    Barbara F 13 65.3 98
    Carol F 14 62.8 102.5
    Henry M 14 63.5 102.5
    James M 12 57.3 83
    Jane F 12 59.8 84.5
    Janet F 15 62.5 112.5
    Jeffrey M 13 62.5 84
    John M 12 59 99.5
    Joyce F 11 51.3 50.5
    Judy F 14 64.3 90
    Louise F 12 56.3 77
    Mary F 15 66.5 112
    Philip M 16 72 150
    Robert M 12 64.8 128
    Ronald M 15 67 133
    Thomas M 11 57.5 85
    William M 15 66.5 112
    ;;;;
    run;quit;

    proc contents data=mydb.math position;
    run;quit;

    LIBNAME mydb clear;


    /**************************************************************************************************************************/
    /*   Altair SLC                                                                                                           */
    /*                                                                                                                        */
    /*  The CONTENTS Procedure for PostgreSQL Table                                                                           */
    /*                                                                                                                        */
    /*  Data Set Name           MATH                                                                                          */
    /*  Member Type             DATA                                                                                          */
    /*                                                                                                                        */
    /*  Engine                  POSTGRESQL ===> SLC PostgreSQL Engine <===                                                    */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  Observations                .                                                                                         */
    /*  Variables               5                                                                                             */
    /*  Indexes                 0                                                                                             */
    /*  Observation Length      33                                                                                            */
    /*  Deleted Observations             0                                                                                    */
    /*  Data Set Type                                                                                                         */
    /*  Label                                                                                                                 */
    /*  Compressed              NO                                                                                            */
    /*  Sorted                  NO                                                                                            */
    /*  Data Representation                                                                                                   */
    /*  Encoding                wlatin1 Windows-1252 Western                                                                  */
    /*                                                                                                                        */
    /*             List of Variables and Attributes in Creation Order                                                         */
    /*                                                                                                                        */
    /*    Number    Variable    Type     Len     Pos    Format                                                                */
    /*  ____________________________________________________________                                                          */
    /*         1    NAME        Char       8       0    $8.                                                                   */
    /*         2    SEX         Char       1       8    $1.                                                                   */
    /*         3    AGE         Num        8       9                                                                          */
    /*         4    HEIGHT      Num        8      17                                                                          */
    /*         5    WEIGHT      Num        8      25                                                                          */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC          13:00 Tuesday, July 14, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas

    NOTE: AUTOEXEC processing completed

    1         LIBNAME mydb POSTGRESQL
    2           USER='postgres'
    3           PASSWORD=XXXXXXXXXXXXXX
    4           SERVER='localhost'
    5           DATABASE='template1'
    NOTE: Library mydb assigned as follows:
          Engine:        POSTGRESQL
          Physical Name: localhost

    6           PRESERVE_TAB_NAMES=YES;
    7         LIBNAME mydb POSTGRESQL
    8           USER='postgres'
    9           SERVER='localhost'
    10          DATABASE='template1'
    NOTE: Library mydb assigned as follows:
          Engine:        POSTGRESQL
          Physical Name: localhost

    11          PRESERVE_TAB_NAMES=YES;

    Altair SLC

    The DATASETS Procedure

         Directory

    Libref    MYDB
    Engine    POSTGRESQL

              Members

                Member    Member
      Number    Name      Type

    ----------------------------

           1    MATH      DATA
    12
    13        proc datasets lib=mydb kill;
    14        run;quit;
    NOTE: Deleting MYDB.math (type=DATA)
    NOTE: Procedure datasets step took :
          real time : 0.237
          cpu time  : 0.046


    15
    16        data mydb.math;
    17        informat
    18           name $8.
    19           sex $1.
    20           age 8.
    21           height 8.
    22           weight 8.
    23           ;
    24        input
    25          name sex age height weight;
    26        cards4;

    NOTE: Data set "MYDB.math" has an unknown number of observation(s) and 5 variable(s)
    NOTE: The data step took :
          real time : 0.302
          cpu time  : 0.000


    27        Alfred M 14 69 112.5
    28        Alice F 13 56.5 84
    29        Barbara F 13 65.3 98
    30        Carol F 14 62.8 102.5
    31        Henry M 14 63.5 102.5
    32        James M 12 57.3 83
    33        Jane F 12 59.8 84.5
    34        Janet F 15 62.5 112.5
    35        Jeffrey M 13 62.5 84
    36        John M 12 59 99.5
    37        Joyce F 11 51.3 50.5
    38        Judy F 14 64.3 90
    39        Louise F 12 56.3 77
    40        Mary F 15 66.5 112
    41        Philip M 16 72 150
    42        Robert M 12 64.8 128
    43        Ronald M 15 67 133
    44        Thomas M 11 57.5 85
    45        William M 15 66.5 112
    46        ;;;;
    47        run;quit;
    48
    49        proc contents data=mydb.math position;
    50        run;quit;
    NOTE: Procedure contents step took :
          real time : 0.032
          cpu time  : 0.000


    NOTE: Libref MYDB has been deassigned.
    51
    52        LIBNAME mydb clear;
    53

    NOTE: Submitted statements took :
          real time : 1.792
          cpu time  : 0.250

    /*____   ____                       _       _
    |___ /  | __ )  __ _ ___  ___   ___| | ___ | | __ _ _ __   __ _ _   _  __ _  __ _  ___
      |_ \  |  _ \ / _` / __|/ _ \ / __| |/ __|| |/ _` | `_ \ / _` | | | |/ _` |/ _` |/ _ \
     ___) | | |_) | (_| \__ \  __/ \__ \ | (__ | | (_| | | | | (_| | |_| | (_| | (_| |  __/
    |____/  |____/ \__,_|___/\___| |___/_|\___||_|\__,_|_| |_|\__, |\__,_|\__,_|\__, |\___|
                                                              |___/             |___/
    SELECT THE FOUR YOUNGEST STUDENTS BY SEX IN MATH CLASS
    */

    libname workx sas7bdat "d:/wpswrkx"; /*--- put this in your autoexec ---*/

    proc datasets lib=workx kill;
    run;

    LIBNAME mydb POSTGRESQL
      USER='postgres'
      SERVER='localhost'
      DATABASE='template1'
      PRESERVE_TAB_NAMES=YES;

    proc sort data=mydb.math out=workx.mathSrt;
      by sex age;
    run;

    /*--- create table youngest4bySex in posgreSQL with 4 youngest students by sex ---*/
    data workx.youngest4bySex;
      retain cnt_students 0;
      set workx.mathSrt;
      by sex age;
      cnt_students = ifn(first.sex,1,cnt_students++1);
      if cnt_students<5;
    run;

    /**************************************************************************************************************************/
    /* WORKX.YOUNGEST4BYSEX total obs=8                                                                                       */
    /*          cnt_                                                                                                          */
    /* Obs    students     NAME     SEX    AGE    HEIGHT    WEIGHT                                                            */
    /*                                                                                                                        */
    /*  1         1       Joyce      F      11     51.3       50.5                                                            */
    /*  2         2       Jane       F      12     59.8       84.5                                                            */
    /*  3         3       Louise     F      12     56.3       77.0                                                            */
    /*  4         4       Alice      F      13     56.5       84.0                                                            */
    /*                                                                                                                        */
    /*  5         1       Thomas     M      11     57.5       85.0                                                            */
    /*  6         2       James      M      12     57.3       83.0                                                            */
    /*  7         3       John       M      12     59.0       99.5                                                            */
    /*  8         4       Robert     M      12     64.8      128.0                                                            */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC          13:34 Tuesday, July 14, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  13:34:51
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.019
          cpu time  : 0.000

    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.000
          cpu time  : 0.015

    NOTE: AUTOEXEC processing completed

    1         LIBNAME mydb POSTGRESQL
    2           USER='postgres'
    3           PASSWORD=XXXXXXXXXXXXXX
    4           SERVER='localhost'
    5           DATABASE='template1'
    NOTE: Library mydb assigned as follows:
          Engine:        POSTGRESQL
          Physical Name: localhost

    6           PRESERVE_TAB_NAMES=YES;
    7
    8         data workx.youngest4bySex;
    9           retain cnt_students 0;
    10          set workx.mathSrt;
    11          by sex age;
    12          cnt_students = ifn(first.sex,1,cnt_students++1);
    13          if cnt_students<5;
    14        run;

    NOTE: 19 observations were read from "WORKX.mathSrt"
    NOTE: Data set "WORKX.youngest4bySex" has 8 observation(s) and 6 variable(s)
    NOTE: The data step took :
          real time : 0.016
          cpu time  : 0.015


    NOTE: Submitted statements took :
          real time : 0.191
          cpu time  : 0.109

    /*  _                         _   _                            _
    | || |    _ __   __ _ ___ ___| |_| |__  _ __ _   _   ___  __ _| |
    | || |_  | `_ \ / _` / __/ __| __| `_ \| `__| | | | / __|/ _` | |
    |__   _| | |_) | (_| \__ \__ \ |_| | | | |  | |_| | \__ \ (_| | |
       |_|   | .__/ \__,_|___/___/\__|_| |_|_|   \__,_| |___/\__, |_|
             |_|                                                |_|
    NOTE PARTITIONING IS NOT SUPPORTED BY SLC SQL
    */

    proc datasets lib=workx kill;
    run;quit;

    proc sql;
      connect to postgresql (
         USER='postgres'
         SERVER='localhost'
         DATABASE='template1'
         PRESERVE_TAB_NAMES=YES
         );
      create table workx.youngest4bysex as
        select * from connection to postgresql (
          select * from
           (
             select
                row_number() over (partition by SEX order by AGE) as rank
                ,*
             from MATH
           ) as ranked
          where rank < 5
        );

      disconnect from postgresql;
    quit;

    proc print data=workx.youngest4bysex;
    run;
    proc contents data=workx.youngest4bysex position;
    run;

    /**************************************************************************************************************************/
    /* Altair SLC                                                                                                             */
    /* LIST: 14:13:56                                                                                                         */
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /* WORKX.YOUNGEST4BYSEX total obs=8                                                                                       */
    /* Obs    RANK    NAME        SEX    AGE    HEIGHT    WEIGHT                                                              */
    /*                                                                                                                        */
    /*  1        1    Joyce        F      11     51.3       50.5                                                              */
    /*  2        2    Jane         F      12     59.8       84.5                                                              */
    /*  3        3    Louise       F      12     56.3       77.0                                                              */
    /*  4        4    Barbara      F      13     65.3       98.0                                                              */
    /*                                                                                                                        */
    /*  5        1    Thomas       M      11     57.5       85.0                                                              */
    /*  6        2    John         M      12     59.0       99.5                                                              */
    /*  7        3    James        M      12     57.3       83.0                                                              */
    /*  8        4    Robert       M      12     64.8      128.0                                                              */
    /*                                                                                                                        */
    /* The CONTENTS Procedure                                                                                                 */
    /*                                                                                                                        */
    /* Data Set Name           YOUNGEST4BYSEX                                                                                 */
    /* Member Type             DATA                                                                                           */
    /* Engine                  SAS7BDAT                                                                                       */
    /* Created                 14JUL2026:14:13:57                                                                             */
    /* Last Modified           14JUL2026:14:13:57                                                                             */
    /* Observations                     8                                                                                     */
    /* Variables               6                                                                                              */
    /* Indexes                 0                                                                                              */
    /* Observation Length      48                                                                                             */
    /* Deleted Observations             0                                                                                     */
    /* Data Set Type                                                                                                          */
    /* Label                                                                                                                  */
    /* Compressed              NO                                                                                             */
    /* Sorted                  NO                                                                                             */
    /* Data Representation     WINDOWS_64                                                                                     */
    /* Encoding                wlatin1 Windows-1252 Western                                                                   */
    /*                                                                                                                        */
    /*               Engine/Host Dependent Information                                                                        */
    /*                                                                                                                        */
    /* Data Set Page Size          4096                                                                                       */
    /* Number of Data Set Pages    1                                                                                          */
    /* First Data Page             1                                                                                          */
    /* Max Obs Per Page            84                                                                                         */
    /* Obs In First Data Page      8                                                                                          */
    /* File Name                   d:\wpswrkx\youngest4bysex.sas7bdat                                                         */
    /* Release Created             9.0101M3                                                                                   */
    /* Host Created                XP_PRO                                                                                     */
    /*                                                                                                                        */
    /*          List of Variables and Attributes in Creation Order                                                            */
    /*                                                                                                                        */
    /* Number    Variable    Type             Len             Pos    Format                                                   */
    /* ________________________________________________________________________                                               */
    /*      1    RANK        Num                8               0    20.                                                      */
    /*      2    NAME        Char               8              32    $8.                                                      */
    /*      3    SEX         Char               1              40    $1.                                                      */
    /*      4    AGE         Num                8               8                                                             */
    /*      5    HEIGHT      Num                8              16                                                             */
    /*      6    WEIGHT      Num                8              24                                                             */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC          14:18 Tuesday, July 14, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas

    NOTE: AUTOEXEC processing completed


    Altair SLC

    The DATASETS Procedure

             Directory

    Libref           WORKX
    Engine           SAS7BDAT
    Physical Name    d:\wpswrkx

                                      Members

                                  Member
      Number    Member Name       Type         File Size      Date Last Modified

    ----------------------------------------------------------------------------

           1    YOUNGEST4BYSEX    DATA              5120      14JUL2026:14:13:56
    1         proc datasets lib=workx kill;
    2         run;quit;
    NOTE: Deleting WORKX.youngest4bysex (type=DATA)
    NOTE: Procedure datasets step took :
          real time : 0.047
          cpu time  : 0.000


    3
    4         proc sql;
    5           connect to postgresql (
    6              USER='postgres'
    7              SERVER='localhost'
    8              DATABASE='template1'
    9              PRESERVE_TAB_NAMES=YES
    10             );
    NOTE: Successfully connected to database POSTGRESQL as alias POSTGRESQL.
    11          create table workx.youngest4bysex as
    12            select * from connection to postgresql (
    13              select * from
    14               (
    15                 select
    16                    row_number() over (partition by SEX order by AGE) as rank
    17                    ,*
    18                 from MATH
    19               ) as ranked
    20              where rank < 5
    21            );
    NOTE: Data set "WORKX.youngest4bysex" has 8 observation(s) and 6 variable(s)
    22
    23          disconnect from postgresql;
    NOTE: Successfully disconnected from database POSTGRESQL.
    24        quit;
    NOTE: Procedure sql step took :
          real time : 0.079
          cpu time  : 0.015


    25
    26        proc print data=workx.youngest4bysex;
    27        run;
    NOTE: 8 observations were read from "WORKX.youngest4bysex"
    NOTE: Procedure print step took :
          real time : 0.000
          cpu time  : 0.000


    28        proc contents data=workx.youngest4bysex position;
    29        run;
    NOTE: Procedure contents step took :
          real time : 0.047
          cpu time  : 0.015


    30
    31
    32

    NOTE: Submitted statements took :
          real time : 0.301
          cpu time  : 0.203

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
