+++
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
date = {{ .Date }}
draft = true
# One sentence: what the talk covers and where it was given.
description = ''
tags = ['OpenTelemetry']
+++

<!-- Add featured.jpg (the title slide works well) to this folder. -->

The following recording is from [EVENT][1]:

{{ `{{< youtubeLite id="VIDEO_ID" label="Play: TITLE" >}}` }}

Slide deck:

{{ `{{< gslides src="https://docs.google.com/presentation/d/.../embed" >}}` }}

[1]: https://example.com
