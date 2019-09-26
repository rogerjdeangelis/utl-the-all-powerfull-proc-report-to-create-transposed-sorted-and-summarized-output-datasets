# utl-the-all-powerfull-proc-report-to-create-transposed-sorted-and-summarized-output-datasets
The all powerfull proc report to create transposed sorted and summarized output datasets 

    The all powerfull proc report to create transposed sorted and summarized output datasets                              
                                                                                                                          
    Although the data is sorted by reagion. That is not needed.                                                           
                                                                                                                          
    FYI Report is often a very powerfull 'proc transpose', can transpose mutiple sets of variables.                       
                                                                                                                          
    *_                   _                                                                                                
    (_)_ __  _ __  _   _| |_                                                                                              
    | | '_ \| '_ \| | | | __|                                                                                             
    | | | | | |_) | |_| | |_                                                                                              
    |_|_| |_| .__/ \__,_|\__|                                                                                             
            |_|                                                                                                           
    ;                                                                                                                     
                                                                                                                          
    data have;                                                                                                            
        retain n 1;                                                                                                       
        do region="Africa", "Asia", "Canada";                                                                             
           n=n+1;                                                                                                         
           do i=1 to n;                                                                                                   
              sales=int(10*uniform(1237)) +1;                                                                             
              returns=int(10*uniform(1237)) +1;                                                                           
              output;                                                                                                     
           end;                                                                                                           
        end;                                                                                                              
        drop i n;                                                                                                         
        stop;                                                                                                             
    run;quit;                                                                                                             
                                                                                                                          
    /*                                                                                                                    
    WORK.HAVE total obs=9        | RULES (counts and percents)                                                            
                                 |                                                                                        
    REGION    SALES    RETURNS   |                                                                                        
                                 |                                                                                        
    Africa      8         10     | RETURNS_    RETURNS_         RETURNS_    RETURNS_                                      
    Africa      6          9     |  COUNT       PCTN              SUM       PCTSUM                                        
                                                                                                                          
                                   8+6=14      0.22=14/(8+6+    19=10+9     0.34=19/(10+9+                                
                                                1+7+6+                        8+10+8+4+                                   
                                               5+7+9+3)=                      1+2+7+5                                     
    Asia        1         10     |                                                                                        
    Asia        7          8     |                                                                                        
    Asia        6          4     |                                                                                        
                                 |                                                                                        
    Canada      5          1     |                                                                                        
    Canada      7          2     |                                                                                        
    Canada      9          7     |                                                                                        
    Canada      3          5     |                                                                                        
                                 |                                                                                        
     SUM       52         56                                                                                              
    */                                                                                                                    
                                                                                                                          
    *            _               _                                                                                        
      ___  _   _| |_ _ __  _   _| |_                                                                                      
     / _ \| | | | __| '_ \| | | | __|                                                                                     
    | (_) | |_| | |_| |_) | |_| | |_                                                                                      
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                     
                    |_|                                                                                                   
    ;                                                                                                                     
                                                                                                                          
    This is not a report it is a dataset                                                                                  
                                                                                                                          
    WORK.WANT total obs=4                                                                                                 
                                                                                                                          
                SALES_     SALES_    SALES_     SALES_    RETURNS_    RETURNS_    RETURNS_    RETURNS_                    
      REGION     COUNT      PCTN       SUM      PCTSUM      COUNT       PCTN         SUM       PCTSUM                     
                                                                                                                          
      Africa       2      0.22222      14      0.26923        2        0.22222       19        0.33929                    
      Asia         3      0.33333      14      0.26923        3        0.33333       22        0.39286                    
      Canada       4      0.44444      24      0.46154        4        0.44444       15        0.26786                    
      Total        9      1.00000      52      1.00000        9        1.00000       56        1.00000                    
                                                                                                                          
    *                                                                                                                     
     _ __  _ __ ___   ___ ___  ___ ___                                                                                    
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                   
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                   
    | .__/|_|  \___/ \___\___||___/___/                                                                                   
    |_|                                                                                                                   
    ;                                                                                                                     
                                                                                                                          
                                                                                                                          
    proc report data=have nowd                                                                                            
          out=want (drop=_break_ rename=(                                                                                 
              _c2_= sales_count                                                                                           
              _c3_= sales_pctn                                                                                            
              _c4_= sales_sum                                                                                             
              _c5_= sales_pctsum                                                                                          
              _c6_= returns_count                                                                                         
              _c7_= returns_pctn                                                                                          
              _c8_= returns_sum                                                                                           
              _c9_= returns_pctsum ));                                                                                    
    column region sales,(n pctn sum pctsum) returns, (n pctn sum pctsum);                                                 
    define region /group ;                                                                                                
    format _numeric_ 8.4;                                                                                                 
    define n        / "";  /* _c2_= sales_count    */                                                                     
    define pctn     / "";  /* _c3_= sales_pctn     */                                                                     
    define sum      / "";  /* _c4_= sales_sum      */                                                                     
    define pctsum   / "";  /* _c5_= sales_pctsum   */                                                                     
    define n        / "";  /* _c6_= returns_count  */                                                                     
    define pctn     / "";  /* _c7_= returns_pctn   */                                                                     
    define sum      / "";  /* _c8_= returns_sum    */                                                                     
    define pctsum   / "";  /* _c9_= returns_pctsum */                                                                     
    rbreak after /summarize style (summary)=Header;                                                                       
    compute after;                                                                                                        
    region='Total';                                                                                                       
    endcomp;                                                                                                              
    run;quit;                                                                                                             
                                                                                                                          
    2041!     quit;                                                                                                       
    NOTE: There were 9 observations read from the data set WORK.HAVE.                                                     
    NOTE: The data set WORK.WANT has 4 observations and 9 variables.                                                      
    NOTE: PROCEDURE REPORT used (Total process time):                                                                     
          real time           0.09 seconds                                                                                
          user cpu time       0.01 seconds                                                                                
                                                                                                                          
                                                                                                                          
