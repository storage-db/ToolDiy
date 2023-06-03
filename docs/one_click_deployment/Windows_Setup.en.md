# windows Environmental deployment

This article shows you how to deploy the project in your windows environment.

 > Note: This requires a python environment, `python3.10` in my case.


## Download ToolDiy

```
git clone https://github.com/cargo-youth/ToolDiy.git
```

## Install mkdocs

```
Download link：pip install mkdocs
```

## Install site theme

The theme of this site is material. Use the following command to install it.

```
pip install mkdocs-material
```

## Install other dependencies

```
pip install pymdown-extensions
pip install mkdocs-awesome-pages-plugin
```

## Install the i18n

Here is a pit, when I install, directly install `pip install i18n` is not ok, you need to specially install i18n under mkdocs, then ask chatGPT, he provided me with a solution is `pip install mkdocs-i18n-plugin` ; Unfortunately, no, finally find the following command on Google, right.

```
pip install mkdocs-static-i18n
```

## Running Project

```
mkdocs serve
```

## Build static website files

```
mkdocs build
```

















