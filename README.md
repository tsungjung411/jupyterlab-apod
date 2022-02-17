# jupyterlab_apod
> - Source: [[jupyterlab] Extension Tutorial](https://jupyterlab.readthedocs.io/en/stable/extension/extension_tutorial.html)
> - Also See: [跟著官方手冊開發 JupyterLab Extension](https://qrtt1.medium.com/677ab218ea2f)

Show an Astronomy Picture of the Day widget

## 官方範例缺點
1. 對初學者來說太難，並不能作為剛接觸 jupyterlab extension 的開發者
2. 初次按一次， `widget.content.update();` 會連發 4 次 requests；
   <br>正常來說，按一次應該就請求 1 次 requests；
   <br>結果：在測試期間容易發出太多次 request，而導致 url 短時時間被禁止存取
   ```json
   {
     "error": {
       "code": "OVER_RATE_LIMIT",
       "message": "You have exceeded your rate limit. Try again later or contact us at https://api.nasa.gov:443/contact/ for assistance"
     }
   }
   ```
3. 官方並無介紹 url response 有哪些情況
   - media_type 有分 image (.jpg, .gif) 和 video (youtube link) 
   - 當 url 被禁用時，error 訊息的格式是如何？
4. `APODResponse` 的宣告是多餘的

<br>

## Requirements

* JupyterLab >= 3.0

## Install

To install the extension, execute:

```bash
pip install jupyterlab_apod
```

## Uninstall

To remove the extension, execute:

```bash
pip uninstall jupyterlab_apod
```


## Contributing

### Development install

Note: You will need NodeJS to build the extension package.

The `jlpm` command is JupyterLab's pinned version of
[yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use
`yarn` or `npm` in lieu of `jlpm` below.

```bash
# Clone the repo to your local environment
# Change directory to the jupyterlab_apod directory
# Install package in development mode
pip install -e .
# Link your development version of the extension with JupyterLab
jupyter labextension develop . --overwrite
# Rebuild extension Typescript source after making changes
jlpm run build
```

You can watch the source directory and run JupyterLab at the same time in different terminals to watch for changes in the extension's source and automatically rebuild the extension.

```bash
# Watch the source directory in one terminal, automatically rebuilding when needed
jlpm run watch
# Run JupyterLab in another terminal
jupyter lab
```

With the watch command running, every saved change will immediately be built locally and available in your running JupyterLab. Refresh JupyterLab to load the change in your browser (you may need to wait several seconds for the extension to be rebuilt).

By default, the `jlpm run build` command generates the source maps for this extension to make it easier to debug using the browser dev tools. To also generate source maps for the JupyterLab core extensions, you can run the following command:

```bash
jupyter lab build --minimize=False
```

### Development uninstall

```bash
pip uninstall jupyterlab_apod
```

In development mode, you will also need to remove the symlink created by `jupyter labextension develop`
command. To find its location, you can run `jupyter labextension list` to figure out where the `labextensions`
folder is located. Then you can remove the symlink named `jupyterlab-apod` within that folder.

### Packaging the extension

See [RELEASE](RELEASE.md)
