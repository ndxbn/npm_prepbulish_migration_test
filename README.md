# npm_prepbulish_migration_test
https://docs.npmjs.com/misc/scripts#prepublish-and-prepare

You can find executed result in https://travis-ci.org/ndxbn/npm_prepbulish_migration_test .

"step 4" and "step 5" means https://github.com/npm/npm/issues/10074 one. 

# Result (command separated)

## npm install

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main |  8  |  8  |  8  |  8  |  9  |  7  | No  | No  
prepublishOnly main | No  | No  | No  | No  | No  | No  | No  | No  
publish        main | No  | No  | No  | No  | No  | No  | No  | No  
postpublish    main | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     main |  1  |  1  |  5  |  2  |  3  |  1  |  1  |  1  
install        main |  6  |  6  |  6  |  6  |  7  |  5  |  5  |  5  
postinstall    main |  7  |  7  |  7  |  7  |  8  |  6  |  6  |  6  
prepack        main | No  | No  | No  | No  | No  | No  | No  | No  
pack           main | No  | No  | No  | No  | No  | No  | No  | No  
postpack       main | No  | No  | No  | No  | No  | No  | No  | No  
prepare        main | No  | No  | No  | No  | 10  |  8  |  7  |  7  
(is_private)   main | No  | No  | No  | No  | No  | No  | No  | No  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  |  2  |  2  |  1  |  1  |  1  | No  | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No  | No  | No  
publish        sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpublish    sub  | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     sub  |  3  |  3  |  2  |  3  |  4  |  2  |  2  |  2  
install        sub  |  4  |  4  |  3  |  4  |  5  |  3  |  3  |  3  
postinstall    sub  |  5  |  5  |  4  |  5  |  6  |  4  |  4  |  4  
prepack        sub  | No  | No  | No  | No  | No  | No  | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepare        sub  | No  | No  | No  | No  |  2  | No  | No  | No  

## npm install foo

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main | No  | No  | No  | No  | No  | No  | No  | No  
prepublishOnly main | No  | No  | No  | No  | No  | No  | No  | No  
publish        main | No  | No  | No  | No  | No  | No  | No  | No  
postpublish    main | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     main | No  | No  | No  | No  | No  | No  | No  | No  
install        main | No  | No  | No  | No  | No  | No  | No  | No  
postinstall    main | No  | No  | No  | No  | No  | No  | No  | No  
prepack        main | No  | No  | No  | No  | No  | No  | No  | No  
pack           main | No  | No  | No  | No  | No  | No  | No  | No  
postpack       main | No  | No  | No  | No  | No  | No  | No  | No  
prepare        main | No  | No  | No  | No  | No  | No  | No  | No  
(is_private)   main | No  | No  | No  | No  | No  | No  | No  | No  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  |  1  |  1  |  1  |  1  |  1  | No  | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No  | No  | No  
publish        sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpublish    sub  | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     sub  |  2  |  2  |  2  |  2  |  3  |  1  |  1  |  1  
install        sub  |  3  |  3  |  3  |  3  |  4  |  2  |  2  |  2  
postinstall    sub  |  4  |  4  |  4  |  4  |  5  |  3  |  3  |  3  
prepack        sub  | No  | No  | No  | No  | No  | No  | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepare        sub  | No  | No  | No  | No  |  2  | No  | No  | No  

## npm publish

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main |  1  |  1  |  1  |  1  |  1  |  1  |  3  |  2  
prepublishOnly main | No  | No  | No  | No  |  3  |  3  |  2  | No (deleted)  
publish        main |  3  |  3  |  3  |  3  |  5  |  7  |  7  |  6 
postpublish    main |  4  |  4  |  4  |  4  |  6  |  8  |  8  |  7 
preinstall     main | No  | No  | No  | No  | No  | No  | No  | No  
install        main | No  | No  | No  | No  | No  | No  | No  | No  
postinstall    main | No  | No  | No  | No  | No  | No  | No  | No  
prepack        main | No  | No  | No  | No  | No  |  4  |  4  |  3  
pack           main | No  | No  | No  | No  | No  | No! | No? | No?  
postpack       main | No  | No  | No  | No  | No  |  5  |  5  |  4  
prepare        main | No  | No  | No  | No  |  2  |  2  |  1  |  1  
(is_private)   main |  2  |  2  |  2  |  2  |  4  |  6  |  6  |  5  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No  | No  | No  
publis         sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpublis     sub  | No  | No  | No  | No  | No  | No  | No  | No  
preinstall     sub  | No  | No  | No  | No  | No  | No  | No  | No  
install        sub  | No  | No  | No  | No  | No  | No  | No  | No  
postinstall    sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepack        sub  | No  | No  | No  | No  | No  | No  | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No  | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No  | No  | No  
prepare        sub  | No  | No  | No  | No  | No  | No  | No  | No  

> 4. In a year or so, make a semver-major bump to npm and make prepublish's behavior match prepublishOnly.

* `prepublish` should run after `prepare` .
* `prepublish` and `prepublishOnly` Should Not Depends. If don't depends,  they can be swapped.

## npm pack

[`prepack` and `postpack` was implemented at v5.0.0](http://blog.npmjs.org/post/161081169345/v500).

npm script stage ＼ version | 2.14.3 | 2.15.11 | 3.8.6 | 3.10.10 | 4.2.0 | 5.6.0 | step 4 | step 5
:-- | --- | --- | --- | --- | --- | --- | --- | ---
prepublish     main |  1  |  1  |  1  |  1  |  1  |  1 | No  | No  
prepublishOnly main | No  | No  | No  | No  | No! | No!| No  | No  
publish        main | No  | No  | No  | No  | No  | No | No  | No  
postpublish    main | No  | No  | No  | No  | No  | No | No  | No  
preinstall     main | No  | No  | No  | No  | No  | No | No  | No  
install        main | No  | No  | No  | No  | No  | No | No  | No  
postinstall    main | No  | No  | No  | No  | No  | No | No  | No  
prepack        main | No  | No  | No  | No  | No  |  3 |  2  |  2  
pack           main | No  | No  | No  | No  | No  | No!| No? | No? 
postpack       main | No  | No  | No  | No  | No  |  4 |  3  |  3  
prepare        main | No  | No  | No  | No  |  2  |  2 |  1  |  1  
(is_private)   main | No  | No  | No  | No  | No  | No | No  | No  
===                 | ==  | ==  | ==  | ==  | ==  | ==  | ==  | ==  
prepublish     sub  | No  | No  | No  | No  | No  | No | No  | No  
prepublishOnly sub  | No  | No  | No  | No  | No  | No | No  | No  
publish        sub  | No  | No  | No  | No  | No  | No | No  | No  
postpublish    sub  | No  | No  | No  | No  | No  | No | No  | No  
preinstall     sub  | No  | No  | No  | No  | No  | No | No  | No  
install        sub  | No  | No  | No  | No  | No  | No | No  | No  
postinstall    sub  | No  | No  | No  | No  | No  | No | No  | No  
prepack        sub  | No  | No  | No  | No  | No  | No | No  | No  
pack           sub  | No  | No  | No  | No  | No  | No | No  | No  
postpack       sub  | No  | No  | No  | No  | No  | No | No  | No  
prepare        sub  | No  | No  | No  | No  | No  | No | No  | No  


# Result (version separated)
## npm v5.6.0 (Node.js v8.9.4 - v9.5.0)

> npm WARN prepublish-on-install As of npm@5, `prepublish` scripts are deprecated.
> npm WARN prepublish-on-install Use `prepare` for build steps and `prepublishOnly` for upload-only.
> npm WARN prepublish-on-install See the deprecation note in `npm help scripts` for more information.


npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main |  7  | No  |  1  |  1 
prepublishOnly main | No  | No  |  3  | No!
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


## npm 4.2.0 (Node.js v7.10.1)


> npm WARN prepublish-on-install As of npm@5, `prepublish` scripts will run only for `npm publish`.
> npm WARN prepublish-on-install (In npm@4 and previous versions, it also runs for `npm install`.)
> npm WARN prepublish-on-install See the deprecation note in `npm help scripts` for more information.

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | ---
prepublish     main |  9  | No  |  1  |  1 
prepublishOnly main | No  | No  |  3  | No!
publis         main | No  | No  | ??? | No 
postpublis     main | No  | No  | ??? | No 
preinstall     main |  3  | No  | No  | No 
install        main |  7  | No  | No  | No 
postinstall    main |  8  | No  | No  | No 
prepack        main | No  | No  | No  | No!
pack           main | No  | No  | No  | No!
postpack       main | No  | No  | No  | No!
prepare        main | 10  | No  |  2  |  2 
(is_private)   main | No  | No  |  4  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  1  |  1  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publis         sub  | No  | No  | No  | No 
postpublis     sub  | No  | No  | No  | No 
preinstall     sub  |  4  |  3  | No  | No 
install        sub  |  5  |  4  | No  | No 
postinstall    sub  |  6  |  5  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  |  2  |  2  | No  | No 


## npm 3.10.10 (Node.js v6.12.3)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | ---
prepublish     main |  8  | No  |  1  |  1 
prepublishOnly main | No  | No  | No  | No 
publish        main | No  | No  | ??? | No 
postpublish    main | No  | No  | ??? | No 
preinstall     main |  2  | No  | No  | No 
install        main |  6  | No  | No  | No 
postinstall    main |  7  | No  | No  | No 
prepack        main | No  | No  | ??? | No!
pack           main | No  | No  | ??? | No!
postpack       main | No  | No  | ??? | No!
prepare        main | No  | No  |  No | No 
(is_private)   main | No  | No  |  2  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  1  |  1  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publish        sub  | No  | No  | No  | No 
postpublish    sub  | No  | No  | No  | No 
preinstall     sub  |  3  |  2  | No  | No 
install        sub  |  4  |  3  | No  | No 
postinstall    sub  |  5  |  4  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 


## npm 3.8.6 (Node.js v5.12.0)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | ---
prepublish     main |  8  | No  |  1  |  1 
prepublishOnly main | No  | No  | No  | No 
publish        main | No  | No  | ??? | No 
postpublish    main | No  | No  | ??? | No 
preinstall     main |  5  | No  | No  | No 
install        main |  6  | No  | No  | No 
postinstall    main |  7  | No  | No  | No 
prepack        main | No  | No  | ??? | No!
pack           main | No  | No  | ??? | No!
postpack       main | No  | No  | ??? | No!
prepare        main | No  | No  | No  | No 
(is_private)   main | No  | No  |  2  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  1  |  1  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publish        sub  | No  | No  | No  | No 
postpublish    sub  | No  | No  | No  | No 
preinstall     sub  |  2  |  2  | No  | No 
install        sub  |  3  |  3  | No  | No 
postinstall    sub  |  4  |  4  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 


## npm 2.15.11 (Node.js v4.8.7)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main |  8  | No  |  1  |  1 
prepublishOnly main | No  | No  | No  | No 
publish        main | No  | No  | ??? | No 
postpublish    main | No  | No  | ??? | No 
preinstall     main |  1  | No  | No  | No 
install        main |  6  | No  | No  | No 
postinstall    main |  7  | No  | No  | No 
prepack        main | No  | No  | ??? | No!
pack           main | No  | No  | ??? | No!
postpack       main | No  | No  | ??? | No!
prepare        main | No  | No  | No  | No 
(is_private)   main | No  | No  |  2  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  2  |  1  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publish        sub  | No  | No  | No  | No 
postpublish    sub  | No  | No  | No  | No 
preinstall     sub  |  3  |  2  | No  | No 
install        sub  |  4  |  3  | No  | No 
postinstall    sub  |  5  |  4  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 


## npm 2.14.3 (iojs)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | --- 
prepublish     main |  8  | No  |  1  |  1 
prepublishOnly main | No  | No  | No  | No 
publish        main | No  | No  | ??? | No 
postpublish    main | No  | No  | ??? | No 
preinstall     main |  1  | No  | No  | No 
install        main |  6  | No  | No  | No 
postinstall    main |  7  | No  | No  | No 
prepack        main | No  | No  | ??? | No!
pack           main | No  | No  | ??? | No!
postpack       main | No  | No  | ??? | No!
prepare        main | No  | No  | No  | No 
(is_private)   main | No  | No  |  2  | No 
===                 | ==  | ==  | ==  | == 
prepublish     sub  |  2  |  1  | No  | No 
prepublishOnly sub  | No  | No  | No  | No 
publish        sub  | No  | No  | No  | No 
postpublish    sub  | No  | No  | No  | No 
preinstall     sub  |  3  |  2  | No  | No 
install        sub  |  4  |  3  | No  | No 
postinstall    sub  |  5  |  4  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 


# template

## npm X.X.X (Node.js vX.X.X)

npm script stage ＼ command | install | install foo | publish | pack
:-- | --- | --- | --- | ---
prepublish     main | No  | No  | No  | No 
prepublishOnly main | No  | No  | No  | No 
publish        main | No  | No  | ??? | No 
postpublish    main | No  | No  | ??? | No 
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
publish        sub  | No  | No  | No  | No 
postpublish    sub  | No  | No  | No  | No 
preinstall     sub  | No  | No  | No  | No 
install        sub  | No  | No  | No  | No 
postinstall    sub  | No  | No  | No  | No 
prepack        sub  | No  | No  | No  | No 
pack           sub  | No  | No  | No  | No 
postpack       sub  | No  | No  | No  | No 
prepare        sub  | No  | No  | No  | No 
