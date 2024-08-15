# hossain.dev
Personal developer site with .dev domain. [Preview Site](https://hossain.dev/)

> TIP: To setup custom domain with GitHub pages, see guideline at https://link.medium.com/GtiJJVEV83 

### Local Development
Run following to validate html page.
```shell script
npx html-validate index.html
```


## Tip
Use following to run local server for development from macOS.
```shell
python -m SimpleHTTPServer 8000

# On new MacOS with Python 3
python3 -m http.server

Then visit: http://localhost:8000/
```

### Run locally from *NIX

Alternative universal way to run it from Windows, MacOS or Linux using npm module.

```shell
npm install --global http-server
http-server ./ -a 127.0.0.1 --port 80 --cors
```
