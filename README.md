# utl_submit_pl64
Interface PERL with SAS/WPS

    ```  Example Read the last record of a file first (or read a file backwards)  ```
    ```    ```
    ```  Mainframe IBM MVS / OS-390 can also read s ile backwards  ```
    ```    ```
    ```  I like DWIM perl witht he Padre editor (all free)  ```
    ```  32bit is more stable with Padre (I switched from 64bit Perl?)  ```
    ```  http://dwimperl.com/windows.html  ```
    ```    ```
    ```  I use Perl for Operating system expanded functionality, 32bit is ok?  ```
    ```    ```
    ```  Good for learnig Perl snippits for all packages;  ```
    ```  https://www.tutorialspoint.com/execute_perl_online.php  ```
    ```    ```
    ```    ```
    ```  HAVE d:/txt/bacwrd.txt  ```
    ```  ======================  ```
    ```    ```
    ```  d:/txt/bacwrd.txt  ```
    ```    ```
    ```  record number 1  ```
    ```  record number 2  ```
    ```  record number 3  ```
    ```  record number 4  ```
    ```  record number 5  ```
    ```  record number 6  ```
    ```  record number 7  ```
    ```  record number 8  ```
    ```  record number 9  ```
    ```  record number 10  ```
    ```    ```
    ```    ```
    ```    ```
    ```  WANT  ```
    ```  ====  ```
    ```    ```
    ```  HAVE d:/log/__log.txt  ```
    ```  =====================  ```
    ```    ```
    ```      record number 10  ```
    ```    ```
    ```  *                _              _       _  ```
    ```   _ __ ___   __ _| | _____    __| | __ _| |_ __ _  ```
    ```  | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |  ```
    ```  | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |  ```
    ```  |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|  ```
    ```  ;  ```
    ```    ```
    ```  data _null_;  ```
    ```    file "d:/txt/bacwrd.txt";  ```
    ```    do rec=1 to 10;  ```
    ```      put  'record number ' rec;  ```
    ```      putlog 'record number ' rec;  ```
    ```    end;  ```
    ```  run;quit;  ```
    ```    ```
    ```  *          _       _   _  ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __  ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \  ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |  ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|  ```
    ```    ```
    ```  ;  ```
    ```    ```
    ```  * backtic separated perl statements;  ```
    ```    ```
    ```  %utl_submit_pl64("  ```
    ```  use File::ReadBackwards ;`  ```
    ```  $bw = File::ReadBackwards->new('d:/txt/bacwrd.txt') or  ```
    ```      die 'cant read file';`  ```
    ```  while( defined( $log_line = $bw->readline ) ) {  ```
    ```      print $log_line ;`  ```
    ```      exit 0;`  ```
    ```  }`  ```
    ```  ");  ```
    ```    ```
    ```  *                _         _  ```
    ```   _ __   ___ _ __| |  _ __ (_)_ __   ___  ```
    ```  | '_ \ / _ \ '__| | | '_ \| | '_ \ / _ \  ```
    ```  | |_) |  __/ |  | | | |_) | | |_) |  __/  ```
    ```  | .__/ \___|_|  |_| | .__/|_| .__/ \___|  ```
    ```  |_|                 |_|     |_|  ```
    ```  ;  ```
    ```    ```
    ```  * have updated this macro to use a backtic to separate perl statements;  ```
    ```    ```
    ```  * drop down to perl;  ```
    ```  %macro utl_submit_pl64(pgm)/des="bactic separated set of py commands";  ```
    ```    * write the program to a temporary file;  ```
    ```    filename pl_pgm "%sysfunc(pathname(work))/pl_pgm.pl" lrecl=32766 recfm=v;  ```
    ```    data _null_;  ```
    ```      length pgm  $32755 cmd $255;  ```
    ```      file pl_pgm ;  ```
    ```      pgm=&pgm;  ```
    ```      semi=countc(pgm,'`');  ```
    ```        do idx=1 to semi;  ```
    ```          cmd=cats(scan(pgm,idx,'`'));  ```
    ```          put cmd $char96.;  ```
    ```          putlog cmd $char96.;  ```
    ```        end;  ```
    ```    run;  ```
    ```    run;quit;  ```
    ```    %let _loc=%sysfunc(pathname(pl_pgm));  ```
    ```    %put &_loc;  ```
    ```    filename rut pipe "D:\Dwimperl\perl\bin\perl &_loc > d:/log/__log.txt";  ```
    ```    data _null_;  ```
    ```      file print;  ```
    ```      infile rut;  ```
    ```      input;  ```
    ```      put _infile_;  ```
    ```    run;quit;  ```
    ```    filename rut clear;  ```
    ```    filename pl_pgm clear;  ```
    ```    data _null_;  ```
    ```      infile "__log.txt";  ```
    ```      input;  ```
    ```      put _infile_;  ```
    ```    run;quit;  ```
    ```  %mend utl_submit_pl64;  ```
    ```    ```
    ```  *_  ```
    ```  | | ___   __ _  ```
    ```  | |/ _ \ / _` |  ```
    ```  | | (_) | (_| |  ```
    ```  |_|\___/ \__, |  ```
    ```  ;  ```
    ```    ```
    ```    ```
    ```  172   %utl_submit_pl64("  ```
    ```  173   use File::ReadBackwards ;`  ```
    ```  174   $bw = File::ReadBackwards->new('d:/txt/bacwrd.txt') or  ```
    ```  175       die 'cant read file';`  ```
    ```  176   while( defined( $log_line = $bw->readline ) ) {  ```
    ```  177       print $log_line ;`  ```
    ```  178       exit 0;`  ```
    ```  179   }`  ```
    ```  180   ");  ```
    ```    ```
    ```  NOTE: The file PL_PGM is:  ```
    ```        Filename=e:\saswork\wrk\_TD4076_BEAST_\pl_pgm.pl,  ```
    ```        RECFM=V,LRECL=32766,File Size (bytes)=0,  ```
    ```        Last Modified=01Jul2017:14:50:59,  ```
    ```        Create Time=01Jul2017:12:17:39  ```
    ```    ```
    ```  use File::ReadBackwards ;  ```
    ```  $bw = File::ReadBackwards->new('d:/txt/bacwrd.txt') or    die 'cant read file';  ```
    ```  while( defined( $log_line = $bw->readline ) ) {    print $log_line ;  ```
    ```  exit 0;  ```
    ```  }  ```
    ```  NOTE: 5 records were written to the file PL_PGM.  ```
    ```        The minimum record length was 96.  ```
    ```        The maximum record length was 96.  ```
    ```  NOTE: DATA statement used (Total process time):  ```
    ```        real time           0.01 seconds  ```
    ```        cpu time            0.01 seconds  ```
    ```    ```
    ```    ```
    ```  e:\saswork\wrk\_TD4076_BEAST_\pl_pgm.pl  ```
    ```    ```
    ```  NOTE: The infile RUT is:  ```
    ```        Unnamed Pipe Access Device,  ```
    ```        PROCESS=D:\Dwimperl\perl\bin\perl e:\saswork\wrk\_TD4076_BEAST_\pl_pgm.pl > d:/log/__log.txt,  ```
    ```        RECFM=V,LRECL=32767  ```
    ```    ```
    ```  NOTE: 0 lines were written to file PRINT.  ```
    ```  NOTE: 0 records were read from the infile RUT.  ```
    ```  NOTE: DATA statement used (Total process time):  ```
    ```        real time           0.11 seconds  ```
    ```        cpu time            0.01 seconds  ```
    ```    ```
    ```    ```
    ```  NOTE: Fileref RUT has been deassigned.  ```
    ```  NOTE: Fileref PL_PGM has been deassigned.  ```
    ```    ```
    ```  NOTE: The infile "__log.txt" is:  ```
    ```        Filename=C:\utl\__log.txt,  ```
    ```        RECFM=V,LRECL=32767,File Size (bytes)=0,  ```
    ```        Last Modified=19Jun2017:15:42:09,  ```
    ```        Create Time=26Jun2017:15:31:29  ```
    ```    ```
    ```  NOTE: 0 records were read from the infile "__log.txt".  ```
    ```  NOTE: DATA statement used (Total process time):  ```
    ```        real time           0.00 seconds  ```
    ```        cpu time            0.00 seconds  ```
