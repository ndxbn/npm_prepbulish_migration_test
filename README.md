# npm_prepbulish_migration_test
https://docs.npmjs.com/misc/scripts#prepublish-and-prepare

You can find executed result in https://travis-ci.org/ndxbn/npm_prepbulish_migration_test .

* `!1` ( Number with prefix "\!") means "execute with WARNING".
* `No!` ( "No" with suffix "\!") means  "I wantta execute, but Not execute actually".

# template

## npm@X.X.X

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main | No  | No  | No  | No 
prepublishOnly main | No  | No  | No  | No 
publis         main | No  | No  | ??? | No 
postpublis     main | No  | No  | ??? | No 
preinstall     main | No  | No  | No  | No 
install        main | No  | No  | No  | No 
postinstall    main | No  | No  | No  | No 
prepack        main | No  | No  | No  | No 
pack           main | No  | No  | No  | No 
postpack       main | No  | No  | No  | No 
prepare        main | No  | No  | No  | No 
(is_private)   main | No  | No  | No  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  | No  | No  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publis         sub  | No  | No  | No  | No 
postpublis     sub  | No  | No  | No  | No 
preinstall     sub  | No  | No  | No  | No 
install        sub  | No  | No  | No  | No 
postinstall    sub  | No  | No  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 

# Result
## npm v5.6.0 (Node.js v9.5.0)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main | !7  | No  | !1  | !1 
prepublishOnly main | No  | No  |  3  | No 
publis         main | No  | No  | ??? | No 
postpublis     main | No  | No  | ??? | No 
preinstall     main |  1  | No  | No  | No 
install        main |  5  | No  | No  | No 
postinstall    main |  6  | No  | No  | No 
prepack        main | No  | No  |  4  |  3 
pack           main | No  | No  | No! | No! 
postpack       main | No  | No  |  5  |  4 
prepare        main |  8  | No  |  2  |  2 
(is_private)   main | No  | No  |  6  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  | No  | No  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publis         sub  | No  | No  | No  | No 
postpublis     sub  | No  | No  | No  | No 
preinstall     sub  |  2  |  1  | No  | No 
install        sub  |  3  |  2  | No  | No 
postinstall    sub  |  4  |  3  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 


TODO ここに追加していく


## npm v2.15.11 (Node.js v4.8.7)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main |  8! | No  |  1  |  1 
prepublishOnly main | No  | No  | No  | No 
publis         main | No  | No  | ??? | No 
postpublis     main | No  | No  | ??? | No 
preinstall     main |  1  | No  | No  | No 
install        main |  6  | No  | No  | No 
postinstall    main |  7  | No  | No  | No 
prepack        main | No  | No  | No  | No 
prepack        main | No  | No  | ??? | No! 
pack           main | No  | No  | ??? | No! 
postpack       main | No  | No  | ??? | No! 
(is_private)   main | No  | No  |  2  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  2! |  1! | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publis         sub  | No  | No  | No  | No 
postpublis     sub  | No  | No  | No  | No 
preinstall     sub  |  3  |  2  | No  | No 
install        sub  |  4  |  3  | No  | No 
postinstall    sub  |  5  |  4  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 


## npm v2.14.3 (iojs)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main |  !8 | No  |  1  |  1 
prepublishOnly main | No  | No  | No  | No 
publis         main | No  | No  | ??? | No 
postpublis     main | No  | No  | ??? | No 
preinstall     main |  1  | No  | No  | No 
install        main |  6  | No  | No  | No 
postinstall    main |  7  | No  | No  | No 
prepack        main | No  | No  | ??? | No! 
pack           main | No  | No  | ??? | No! 
postpack       main | No  | No  | ??? | No! 
prepare        main | No  | No  | No  | No 
(is_private)   main | No  | No  |  2  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  2! |  1! | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publis         sub  | No  | No  | No  | No 
postpublis     sub  | No  | No  | No  | No 
preinstall     sub  |  3  |  2  | No  | No 
install        sub  |  4  |  3  | No  | No 
postinstall    sub  |  5  |  4  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 

