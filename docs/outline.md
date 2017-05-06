# Larpsmith

The goal of Larpsmith is to turn a directory of plain-text character sheets into a nicely-formatted set of PDFs to send out to players. It will also do auxiliary tasks like ensuring relationships map up, drawing relationships, and providing "includes", for when multiple characters have the same text on their character sheets.

Larpsmith is a command line interface (CLI) program. You can create a new Larpsmith project by running `lsm create [PROJECTNAME]`, and you can render this project with `lsm render` while located inside the larpsmith project directory.

## Why?

* The current state of the art in Larp-writing is either Google Docs, Word .doc or .rtf files on dropbox, or something like [Larpwriter](http://www.larpwriter.com/en/), which is slowly becoming out of date.
* Plain text is easy to sync! Whether with systems like Dropbox, or version control like git or mercurial.
* It's hard to maintain style across twenty or more character sheets.
* A lot of the issues in Larp-writing stem not from the characters themselves, but from the interactions and relationships between them (factions, asymmetric relationships, disconnected characters, etc.).

## How?

Documents are divided into two types:

* **Characters**, which will be rendered to PDF, and
* **Includes**, which will not themselves be rendered to PDF, but can be included in character files.

All documents are written in a modified version of markdown which, originally, I will call Larpsmith markup (`.lmu` extension). This syntax looks exactly the same as markdown, but also supports custom syntax (in double curly-braces, `{{}}`) to show where Larpsmith should include common text, or where we are defining relationships to other characters.

In addition, each character file must start with a metadata block, written in yaml. This **must** give the character an ID, and may supply other variables. At the time of writing, I would like to support variables on character objects that can be referenced in both this and other character sheets. This would allow the author of the Larp to change character names and genders quickly, ensuring they don't accidentally mis-gender a character on someone else's sheet.

The general process of rendering a Larpsmith project to file consists of the following steps:

1. Load all includes into file.
2. Load all characters into file (includes populating variables).
3. Render each character as a PDF and output to file.

Step three will take a bit of time: I don't believe there's an easy way to convert markdown into a PDF.

## Roadmap

Once we have the core functionality of Larpsmith working, I would be interested in:

* Developing a tool to examine outgoing/incoming relationships for a character ("I say I'm best friends with that other character, what does their sheet say about me?")
* Developing a weighted graph of relationships ("Who has relationships with whom?")

## To do

* Build basic framework (as a gem).
* Create the `lsm` binary.
* Build the `lsm create` command.
* Build the `lsm render` command.
  * Build the capability to load includes.
  * Build the capability to load + parse character files.
  * Build something to turn markdown into PDF (via the gem `prawn`).