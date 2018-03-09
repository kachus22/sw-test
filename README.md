# Angular Service Worker Test

When I try to implement a `SPA`, I have a problem with the `Service Worker`.

Then I went to find the solution and found something.

this
[[ServiceWorker] localhost took too long to respond. HTTP ERROR 504](https://github.com/angular/angular/issues/21636)

and this
[bug(service-worker): `/` path is omitted by ngsw-config](https://github.com/angular/angular/issues/19945)

then link to here
[How to handle routing in Angular 5+ Service Workers?
](https://stackoverflow.com/questions/48565629/how-to-handle-routing-in-angular-5-service-workers)

and then get this file:
[fix-sw.js](https://gist.github.com/jackkoppa/0f2b5e8cd683a5261037c685ad8bcc8b)
and i found it here
[cityAQ](https://jackkoppa.github.io/cityaq/search)
, it works so perfectly. so i try to use `fix-sw.js`.

but sadly, this does not work for me.~~(At the time I was developing https://zipengye.github.io/)~~

`Cache Storage` -> `ngsw:*:assets:app:cache` cache only `*.ico` and `*.bundle.js`

`*.bundle.css` and the most important `index.html` is not cached.

and then i try to create a new project ~~to rule out my bad coding habits~~.[sw-test](https://github.com/ZiPengYe/sw-test)

however, it still does not work.

`problem 1`:(and https://github.com/ZiPengYe/sw-test/ load `ngsw-worker.js` from https://github.com/ZiPengYe/)
so i fixed it from `main.*.bundle.js`

then i did a lot of attempts, including:

copy directly from [jackkoppa/cityaq(gh-pages)](https://github.com/jackkoppa/cityaq) some files that affect the service worker...and so on.

finally I gave up.

Because (i'm noob) I don't understand the working principle of the service worker, I only know that it is an offline technology or caching technology. So I can only refer to the solution from someone else's code.

However, I could not fall asleep without solving this problem. I still tried to find out what went wrong by using breakpoint debugging (refreshing the page repeatedly).

Do not use `fix-sw.js` first.
and after the `service worker` caches, run `offline`.

After a series of refreshes, I found that the final error occurred [here](https://github.com/ZiPengYe/sw-test/blob/gh-pages/ngsw-worker.js#L2468).

Then look up for related calls.

because [here(appVersion is null)](https://github.com/ZiPengYe/sw-test/blob/gh-pages/ngsw-worker.js#L1950),

because [here(this.state is 1 not 0)](https://github.com/ZiPengYe/sw-test/blob/gh-pages/ngsw-worker.js#L2164),

because [here(chage this.state)](https://github.com/ZiPengYe/sw-test/blob/gh-pages/ngsw-worker.js#L2295)

## Usage
```bash
git clone https://github.com/ZiPengYe/sw-test.git
cd sw-test
npm i --no-optional
# replace YOUR_PATH as https://zipengye.github.io/sw-test/
git -prod -bh YOUR_PATH && node build/fix-sw
```

##
`npm ls --depth=0`
list:
```
+-- @angular/animations@5.2.7
+-- @angular/cli@1.7.2
+-- @angular/common@5.2.7
+-- @angular/compiler@5.2.7
+-- @angular/compiler-cli@5.2.7
+-- @angular/core@5.2.7
+-- @angular/forms@5.2.7
+-- @angular/http@5.2.7
+-- @angular/language-service@5.2.7
+-- @angular/platform-browser@5.2.7
+-- @angular/platform-browser-dynamic@5.2.7
+-- @angular/router@5.2.7
+-- @angular/service-worker@5.2.7
+-- core-js@2.5.3
+-- replace-in-file@3.1.1
+-- rxjs@5.5.6
+-- typescript@2.5.3
`-- zone.js@0.8.20
```

`npm --version`: `5.7.1`

`ng --version`
list:
```
Angular CLI: 1.7.2
Node: 8.9.4
OS: win32 x64
Angular: 5.2.7
```
