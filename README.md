# Unix Manpages in Markdown

## An attempt to provide converted manpages in markdown format.

I'm actually fairly new to manpages as a format, but very familiar with Markdown. Frankly, I expected to find a whole bunch of redundant projects like this one, but have come up emptyhanded.

So far, I've used [mandoc](https://en.wikipedia.org/wiki/Mandoc) via SSH from my iPad to a shared macOS-running machine using a [Siri Shortcut](https://github.com/softwarehistorysociety/mdman/raw/main/MarkdownManpagesMac.shortcut).

Inspired by [this guide](https://wiert.me/2020/03/09/macos-converting-a-man-page-to-markdown/), my shortcut is using the following command to send markdown-formatted results to stdout:

```
mandoc -T markdown `man -w Repeat Item`
```