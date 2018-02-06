```ShellSession
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm --version
2.15.11
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm publish --access=public

> @ndxbn/npm_prepbulish_migration_test@0.0.0 prepublish /home/vagrant/tmp/npm_prepbulish_migration_test
> echo main project prepublish

main project prepublish
+ @ndxbn/npm_prepbulish_migration_test@0.0.0

> @ndxbn/npm_prepbulish_migration_test@0.0.0 publish .
> echo main project publish

main project publish

> @ndxbn/npm_prepbulish_migration_test@0.0.0 postpublish .
> echo main project postpublish

main project postpublish

```

```ShellSession
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm --version
3.8.6
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm publish --access=public

> @ndxbn/npm_prepbulish_migration_test@0.0.1 prepublish /home/vagrant/tmp/npm_prepbulish_migration_test
> echo main project prepublish

main project prepublish
+ @ndxbn/npm_prepbulish_migration_test@0.0.1

> @ndxbn/npm_prepbulish_migration_test@0.0.1 publish .
> echo main project publish

main project publish

> @ndxbn/npm_prepbulish_migration_test@0.0.1 postpublish .
> echo main project postpublish

main project postpublish
```


```ShellSession
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm --version
3.10.10
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm publish --access=public

> @ndxbn/npm_prepbulish_migration_test@0.0.2 prepublish /home/vagrant/tmp/npm_prepbulish_migration_test
> echo main project prepublish

main project prepublish
+ @ndxbn/npm_prepbulish_migration_test@0.0.2

> @ndxbn/npm_prepbulish_migration_test@0.0.2 publish .
> echo main project publish

main project publish

> @ndxbn/npm_prepbulish_migration_test@0.0.2 postpublish .
> echo main project postpublish

main project postpublish
```


```ShellSession
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm --version
4.2.0
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm publish --access=public
npm WARN prepublish-on-install As of npm@5, `prepublish` scripts will run only for `npm publish`.
npm WARN prepublish-on-install (In npm@4 and previous versions, it also runs for `npm install`.)
npm WARN prepublish-on-install See the deprecation note in `npm help scripts` for more information.

> @ndxbn/npm_prepbulish_migration_test@0.0.3 prepublish /home/vagrant/tmp/npm_prepbulish_migration_test
> echo main project prepublish

main project prepublish

> @ndxbn/npm_prepbulish_migration_test@0.0.3 prepare /home/vagrant/tmp/npm_prepbulish_migration_test
> echo main project prepare

main project prepare

> @ndxbn/npm_prepbulish_migration_test@0.0.3 prepublishOnly .
> echo main project prepublishOnly

main project prepublishOnly
+ @ndxbn/npm_prepbulish_migration_test@0.0.3

> @ndxbn/npm_prepbulish_migration_test@0.0.3 publish .
> echo main project publish

main project publish

> @ndxbn/npm_prepbulish_migration_test@0.0.3 postpublish .
> echo main project postpublish

main project postpublish
```


```ShellSession
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm --version
5.6.0
vagrant@ndxbn:~/tmp/npm_prepbulish_migration_test$ npm publish --access=public
npm WARN prepublish-on-install As of npm@5, `prepublish` scripts are deprecated.
npm WARN prepublish-on-install Use `prepare` for build steps and `prepublishOnly` for upload-only.
npm WARN prepublish-on-install See the deprecation note in `npm help scripts` for more information.

> @ndxbn/npm_prepbulish_migration_test@0.0.4 prepublish .
> echo main project prepublish

main project prepublish

> @ndxbn/npm_prepbulish_migration_test@0.0.4 prepare .
> echo main project prepare

main project prepare

> @ndxbn/npm_prepbulish_migration_test@0.0.4 prepublishOnly .
> echo main project prepublishOnly

main project prepublishOnly

> @ndxbn/npm_prepbulish_migration_test@0.0.4 prepack .
> echo main project prepack

main project prepack

> @ndxbn/npm_prepbulish_migration_test@0.0.4 postpack .
> echo main project postpack

main project postpack

> @ndxbn/npm_prepbulish_migration_test@0.0.4 publish .
> echo main project publish

main project publish

> @ndxbn/npm_prepbulish_migration_test@0.0.4 postpublish .
> echo main project postpublish

main project postpublish
+ @ndxbn/npm_prepbulish_migration_test@0.0.4
```
