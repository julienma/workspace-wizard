# iTermocil-launcher

> [iTermocil](https://github.com/TomAnthony/itermocil) allows you to setup pre-configured layouts of windows and panes in iTerm2, having each open in a specified directory and execute specified commands. You do this by writing YAML files.

This launcher allows you to run those scripts *without even being* in your terminal. The whole point for iTermocil being to open that terminal for me.

That's an Automator app, which just take a `*.itermocil` file as an argument and run it.

## Install

1. [Install iTermocil](https://github.com/TomAnthony/itermocil#installing-itermocil). Make sure it's ok:

    ```sh
    itermocil --version
    # 0.1.8
    ```

2. [Create an iTermocil layout](https://github.com/TomAnthony/itermocil#examples), and make sure to give it the `.itermocil` extension, instead of the default `.yaml`.

    E.g. `whatever.itermocil`:

    ```yaml
    # whatever.itermocil: 2 panes, open finder source folder, ST, gulp
    windows:
      - name: sample-two-panes
        root: ~/Code/sample/www
        layout: even-horizontal
        panes:
          - commands:
            - open .
            - subl .
            - git status
            # Force open a new default browser window
            - sleep 2
            - open -n 'http:' ; sleep 0.5 ; open http://www.google.com
          - commands:
            - gulp
    ```

3. [Download iTermocil.app](https://github.com/julienma/itermocil-launcher/releases/download/v0.1.0/iTermocil-v0.1.0.zip) (the Automator app), and copy it to your `/Applications` folder.

4. Associate iTermocil.app with `*.itermocil` files: right-click on your new `whatever.itermocil` file > Get Info > Open with > select `iTermocil.app` > click "Change All".

## Usage

Just double-click on any of your `*.itermocil` file, and the script will be run.

## Create your own Automator app

Open Automator, create a new Application.
Add a "Run a shell script" step with these parameters:
- shell: `/bin/bash`
- input: arguments
- code:

```sh
export PATH=/usr/local/bin:$PATH
itermocil --layout $1
```

Then save as an .app, copy a nice custom icon (like [this one](https://dribbble.com/shots/1343859-iTerm2-Icon)), and profit.

---

## Credits

- iTerm2 Icon by [Dax Hansen](https://dribbble.com/shots/1343859-iTerm2-Icon).
