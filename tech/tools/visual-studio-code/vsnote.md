# vsNote

#### extension 설치

* [vsNotes](https://marketplace.visualstudio.com/items?itemName=patricklee.vsnotes)
* [vsnote-template](https://blog.chick-p.work/blog/vsnote-template)

#### Snippet Template 생성

* [Snippet](https://code.visualstudio.com/docs/editor/userdefinedsnippets)
* [Snippet-template](https://qiita.com/ysmb-wtsg/items/6863d853174b46f9dc34)

`ctrl+shift+p` > Snippets:configure User Snippets > markdown.json

```md
{
	"vsnote_template_blog": {
		"prefix": "vsnote_template_blog",
		"body": [
			"---",
			"hide_table_of_contents: false",
			"title: ${TM_FILENAME_BASE}",
			"directory: ${TM_DIRECTORY/^.+\\\\(.*)$/$1/}",
			"date: $CURRENT_YEAR-$CURRENT_MONTH-$CURRENT_DATE $CURRENT_HOUR:$CURRENT_MINUTE:$CURRENT_SECOND",
			"authors: ysyoo",
			"tags:",
			" - note",
			"---",
            "\n# $1",
			"",
			"## content1",
		]
	}
}
```

`ctrl+shift+p` > Open User Settings(settings.json)

```md
{
    "vsnotes.defaultNoteTitle": "{dt}-{title}.{ext}",   // '{dt}-{title}' 형태로 변경
    "vsnotes.defaultNotePath": "~/Documents/Github/ha-ving.github.io/blog/",
    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "vsnotes.defaultSnippet": {
        "langId": "markdown",
        "name": "vsnotes"
    },
    "vsnotes.templates": [
        "blog"
    ],
    "vsnotes.noteTitleConvertSpaces": " ",
    "vsnotes.tokens": [
      {
        "type": "datetime",
        "token": "{dt}",
        "format": "YYYY-MM-DD",                         // 'YYYY-MM-DD' 형태로 변경
        "description": "Insert formatted datetime."
      },
      {
        "type": "title",
        "token": "{title}",
        "description": "Insert note title from input box.",
        "format": "Untitled"
      },
      {
        "type": "extension",
        "token": "{ext}",
        "description": "Insert file extension.",
        "format": "md"
      }
    ],
}
```

#### settings 수정

1. setting > preference > vsNotes > vsnotes: `vsnote workspace directory 설정`
2. setting > preference > vsNotes > vsnotes Templates > `add Item`&#x20;
