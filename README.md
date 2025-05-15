# utl-handy-little-macro-to-format-statistical-confidence-intervals
Handy little macro to format statistical confidence intervals
    %let pgm=utl-handy-little-macro-to-format-statistical-confidence-intervals;

    %stop_submission;

    Handy little macro to format statistical confidence intervals

    github
    https://tinyurl.com/2etnfeex
    https://github.com/rogerjdeangelis/utl-handy-little-macro-to-format-statistical-confidence-intervals

    Note: This macro uses a referback to previous macro argument value.
          If you do not supply a a format for the "mean" it
          defaults to the format for the lower and upper format.


    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    /**************************************************************************************************************************/
    /*       INPUT           |                           PROCESS                                     |    OUTPUT              */
    /*                       |                                                                       |                        */
    /* WORK.HAVE total obs=4 | data want;                                                            | WORK.WANT total obs=4  */
    /*                       |   length ci $44;                                                      |                        */
    /*   mid   lwr   upr     |   set have;                                                           | CI                     */
    /*                       |   select(_n_);                                                        |                        */
    /*  2.00  1.00  3.00     |     when (1) ci=%utl_ci(mid,lwr,upr,LwrUpr_format=1.);                | 2 (1, 3)               */
    /*  2.00  1.50  3.50     |     when (2) ci=%utl_ci(mid,lwr,upr,LwrUpr_format=3.1,mid_format=1.); | 2 (1.5, 3.5)           */
    /*  1.03  1.01  1.04     |     when (3) ci=%utl_ci(mid,lwr,upr,LwrUpr_format=5.2);               | 1.03 (1.01, 1.04)      */
    /*  1.50  1.00  2.00     |     when (4) ci=%utl_ci(mid,lwr,upr,LwrUpr_format=1.,mid_format=3.1); | 1.5 (1, 2)             */
    /*                       |     otherwise;                                                        |                        */
    /* data have;            |   end;                                                                |                        */
    /*   input mid lwr upr;  | run;quit;                                                             |                        */
    /* cards4;               |                                                                       |                        */
    /* 2 1 3                 |                                                                       |                        */
    /* 2 1.5 3.5             | save macro in autocall folder c:/oto/utl_ci.sas                       |                        */
    /* 1.03 1.01 1.04        |                                                                       |                        */
    /* 1.5 1 2               | filename ft15f001 "c:/oto/utl_ci.sas";                                |                        */
    /* ;;;;                  | parmcards4;                                                           |                        */
    /* run;quit;             | %macro utl_ci(                                                        |                        */
    /*                       |        Mid                                                            |                        */
    /*                       |       ,Lwr                                                            |                        */
    /*                       |       ,Upr                                                            |                        */
    /*                       |       ,LwrUpr_format=4.1                                              |                        */
    /*                       |       ,mid_format=&LwrUpr_format                                      |                        */
    /*                       |       )                                                               |                        */
    /*                       |    / des="standard confidence interval formatting";                   |                        */
    /*                       |       compbl(put(&Mid,&mid_format -l)                                 |                        */
    /*                       |        !!' ('                                                         |                        */
    /*                       |        !!compress(put(&Lwr,&LwrUpr_format -l)                         |                        */
    /*                       |        !!',')                                                         |                        */
    /*                       |        !!' '                                                          |                        */
    /*                       |        !!put(&Upr,&LwrUpr_format -r)                                  |                        */
    /*                       |        !!')')                                                         |                        */
    /*                       | %mend utl_ci;                                                         |                        */
    /*                       | ;;;;                                                                  |                        */
    /*                       | run;quit;                                                             |                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

