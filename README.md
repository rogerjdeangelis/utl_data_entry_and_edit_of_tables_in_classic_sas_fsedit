# utl_data_entry_and_edit_of_tables_in_classic_sas_fsedit
Data Entry and edit of tables in Classic SAS FSEDIT.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.


    Data Entry and edit of tables in Classic SAS FSEDIT;

    Note fsedit supports a second set of function keys

    This can be changed to add records.

    You might want to google SAS FSEDIT data entry

    github
    https://tinyurl.com/yazb3skp
    https://github.com/rogerjdeangelis/utl_data_entry_and_edit_of_tables_in_classic_sas_fsedit

    https://tinyurl.com/y9mdv9gf
    https://communities.sas.com/t5/SASware-Ballot-Ideas/Data-Entry-in-EG-and-SAS-Studio/idi-p/475913


    INPUT
    =====

    CLASS dataset

    Up to 40 obs from class total obs=19

    Obs    NAME        SEX AGE HEIGHT WEIGHT

      1    Alfred       M   89     69  112.5

      2    Alice        F   13   56.5     84

      3    Barbara      F   13   65.3     98
      4    Carol        F   14   62.8  102.5


    EXAMPLE OUTPUT
    --------------
    2 or next(function key)

    Obs    NAME        SEX AGE HEIGHT WEIGHT

      1    Alfred       M   89     69  112.5

      2    Added        X   33     44     55   ** changed

      3    Barbara      F   13   65.3     98
      4    Carol        F   14   62.8  102.5


    PROCESS
    =======

    Look at tool taskbar for mavigation or better learn some simple commands.

    %symdel name xist;
    data _null_;
        * get dataset name and existance status;
        rc=dosubl('
          %symdel name xist;
          data _null_;
            window dsn irow=1 rows=12 color=white
              #3 @10
              "DatasetName:" +1 name $44.;
            display dsn;
            call symputx("name",name);
            stop;
            run;quit;
          data _null_;
            put "&name";
            xis=exist("&name");
            put xis=;
            xist=put(xis,1.);
            put xist=;
            call symputx("xist",xist);
          run;quit;
           ');
        dsn=symget('name');
        xis=symget('xist');
        put dsn=;
        put xis=;
        * if dataset exits then edit it;
        if xis='1' then do;
           rc=dosubl('
             proc print data=&name(obs=3);
             run;quit;
             proc fsedit data=&name;
             run;quit;
             proc print data=&name(obs=3);
             run;quit;
           ');
        end;
        else do;
            window dne irow=1 rows=12 color=white
              #3  @10 'Dataset Does not exist'
                      color=black
              #5 @10 'Press ENTER to end interaction';
          display dne;
        end;
       stop;
    run;quit;

    +--------------------------------------------------+
    |===>                                              |
    |                                                  |
    |                                                  |
    |   Enter Datset name ___class________________     |
    |                                                  |
    |                                                  |
    +--------------------------------------------------+


    +--------------------------------------------------+
    |===> end (after edit)                             |
    |                                                  |
    |                                                  |
    |                                                  |
    |  NAME         Jeffrey (change to Roger)          |
    |  SEX          M                                  |
    |  AGE          13                                 |
    |  HEIGHT       62.5                               |
    |  WEIGHT       84                                 |
    |                                                  |
    |                                                  |
    +--------------------------------------------------+


    OUTPUT
    ======

    After you enter the dataset to edit use
    command line for navigation.

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    Data class;
     set sashelp.class;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see process

