# utl-counts-of-strings-of-contiguous-numbers-that-are-the-same-rle-runs
Counts of strings of contiguous numbers that are the same (runn length encoding)

    Counts of strings of contiguous numbers that are the same (runn length encoding)

    github
    https://tinyurl.com/y8n9bdsv
    https://github.com/rogerjdeangelis/utl-counts-of-strings-of-contiguous-numbers-that-are-the-same-rle-runs

    https://tinyurl.com/y9snecu7
    https://stackoverflow.com/questions/52674624/how-to-find-strings-of-contiguous-numbers-that-are-the-same

    Maurits Evers profile
    https://stackoverflow.com/users/6530970/maurits-evers


    INPUT
    =====

    SD1.HAVE total obs=16
                          | RULE
     A    B    C          |
                          |
     0    1    0          |
     1    1    0          |
     1    1    0          |
     1    1    0          |
     1    0    0          |

     0    0    1          |  C has only 1 run of 1s
     0    0    1          |
     1    0    1          |
     1    0    1          |
     1    1    1          |
     0    1    1          |
     0    1    1          |

     1    1    0          |
     1    1    0          |
     1    0    0          |
     1    0    0          |


    EXAMPLE OUTPUT
    --------------

     VARS    CONTIG

      A         3     3 runs od 1s in col A
      B         2
      C         1


    PROCESS
    ========

    %utl_submit_r64('
    library(haven);
    library(SASxport);
    have<-read_sas("d:/sd1/have.sas7bdat");
    want<-as.data.frame(sapply(have, function(x) sum(rle(x)$values == 1)));
    want$VARS<- rownames(want);
    want$CONTIG<-want[,1];
    want<-want[,-1];
    write.xport(want,file="d:/xpt/want.xpt");
    ');

    libname xpt xport "d:/xpt/want.xpt";

    proc print data=xpt.want ;
    run;quit;

    OUTPUT
    ======

    see above

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     input A B C ;
    cards4;
    0 1 0
    1 1 0
    1 1 0
    1 1 0
    1 0 0
    0 0 1
    0 0 1
    1 0 1
    1 0 1
    1 1 1
    0 1 1
    0 1 1
    1 1 0
    1 1 0
    1 0 0
    1 0 0
    ;;;;
    run;quit;



