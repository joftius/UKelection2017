The 2017 UK General Election
================

Load the data
-------------

``` r
data <- read.csv("GE2017 - Constituency results - Sheet1.csv",
                 skip = 1, header=T, stringsAsFactors = F)
data[,7:15] <- lapply(data[,7:15],function(x){as.numeric(gsub(",", "", x))})
data[is.na(data)] <- 0
con <- data %>% filter(X2017 == "Con")
lab <- data %>% filter(X2017 == "Lab")
nrow(con)
```

    ## [1] 317

Labour's weakest seats
----------------------

Among seats won by Labour, how many might Con + UKIP have won?

``` r
labmargin <- with(lab, Con + UKIP - Lab)
sum(labmargin > 0)
```

    ## [1] 9

And how many would have been won by a margin of 1000?

``` r
sum(labmargin > 1000)
```

    ## [1] 5

Which seats are these?

``` r
print(lab[which(labmargin > 1000), c(1,7,8,12)], row.names = FALSE)
```

    ##              Constituency   Con   Lab UKIP
    ##                  Ashfield 20844 21285 1885
    ##          Crewe & Nantwich 25880 25928 1885
    ##              Dudley North 18068 18090 2144
    ##                  Keighley 23817 24066 1291
    ##  Penistone & Stocksbridge 21485 22807 3453

Tories weakest seats
--------------------

``` r
conmargin <- with(con, Lab + LDem + SNP - Con)
sum(conmargin > 0)
```

    ## [1] 52

And how many would have been won by a margin of 1000?

``` r
sum(conmargin > 1000)
```

    ## [1] 33

Which seats are these?

``` r
print(con[which(conmargin > 1000), c(1,7:10)], row.names = FALSE)
```

    ##                     Constituency   Con   Lab  LDem   SNP
    ##                         Broxtowe 25983 25120  2247     0
    ##                       Colchester 24565 18888  9087     0
    ##                        St Albans 24571 13137 18462     0
    ##                          Watford 26731 24639  5335     0
    ##                  Chipping Barnet 25679 25326  3012     0
    ##   Cities of London & Westminster 18005 14857  4270     0
    ##         Finchley & Golders Green 24599 22942  3463     0
    ##                           Putney 20679 19125  5448     0
    ##                    Richmond Park 28588  5773 28543     0
    ##                        Wimbledon 23946 18324  7427     0
    ##                          Cheadle 24331 10417 19824     0
    ##                      Hazel Grove 20047  9036 14533     0
    ##                        Southport 18541 15627 12661     0
    ##                   Aberdeen South 18746  9143  2600 13994
    ##                            Angus 18148  5233  1308 15504
    ##           Ayr, Carrick & Cumnock 18550 11024   872 15776
    ##                   Banff & Buchan 19976  3936  1448 16283
    ##              Dumfries & Galloway 22344 10775  1241 16701
    ##                East Renfrewshire 21496 14346  1112 16784
    ##                           Gordon 21861  6340  6230 19254
    ##                            Moray 22637  5208  1078 18478
    ##         Ochil & South Perthshire 22469 10847  1742 19110
    ##                         Stirling 18291 10902  1683 18143
    ##  West Aberdeenshire & Kincardine 24704  5706  4461 16754
    ##                   Hastings & Rye 25668 25322  1885     0
    ##              Southampton, Itchen 21773 21742  1421     0
    ##               Camborne & Redruth 23001 21424  2979     0
    ##                       Cheltenham 26615  5408 24046     0
    ##                      North Devon 25517  7063 21185     0
    ##                          St Ives 22120  7298 21808     0
    ##                 Truro & Falmouth 25123 21331  8465     0
    ##                    Calder Valley 26790 26181  1952     0
    ##                           Pudsey 25550 25219  1761     0

Conclusion
----------

It seems pretty safe to say the Conservatives would have **at least 20 fewer seats**, taking them well below the required majority, if Labour, Lib Dem, and SNP voters had coordinated.

**This is a failure of [First-past-the-post](https://en.wikipedia.org/wiki/First-past-the-post_voting) voting systems**.

It is very difficult to communicate with all voters supporting several different parties to get them to adopt a strategy.

**[Better voting systems](https://en.wikipedia.org/wiki/Instant-runoff_voting) accomplish the strategic outcome automatically** and should be a top priority for everyone who supports democracy.
