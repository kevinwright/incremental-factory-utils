# incremental-factory-utilities

This app is written in FP-style Scala, this is non-negotiable.

## Setup

To run, first install SBT (use SDKMan for this on MacOS or Linux).
Then launch the console via `sbt`

It makes two commands available

## Save Analysis

    run analyse-save-file --intent all classpath:/savegame-reference.json

This analyses the embedded save file, to use a real one change the `classpath...`
argument to point to it.  `--intent` can be `buildings|resources|skills|all`
or just the first letter of these, and you can repeat the `--intent` argument more than once.

e.g.

    -i b -i r

## Wiki Publishing

To publish to the wiki you'll need a credentials file. For wiki.gg use this template:

    basic-user=<ask @severin>
    basic-pass=<ask @severin>
    wiki-user=<YourName>@<botname>
    wiki-pass=<Your Bot Password>
    url-base=https://incrementalfactory.wiki.gg
    rest-path=rest.php/v1
    api-path=api.php

**DO NOT** badger people for wiki.gg credentials whilst that site is not
yet publicly open. First demonstrate on fandom that you're willing and able
to make a meaningful contribution.

For fandom:

    wiki-user=<YourName>@<botname>
    wiki-pass=<Your Bot Password>
    url-base=https://incremental-factory.fandom.com/
    rest-path=rest.php/v1
    api-path=api.php%

A bot password can be created in the wiki at `/wiki/Special:BotPasswords`

The app looks for this file in `~/incremental-factory-wiki.credentials` by default,
but this path can be overridden via a command line arg.


The command (inside the SBT console) is then

    run publish-wiki --intent buildings --credentials /Users/me/incremental-factory-fandom.credentials

The intent options here are `main`, `items`, `buildings`, `parceltypes`, `skills`,  and `all`

### Rate-Limiting

Unless running as an administrator, fandom has some harsh rate-limiting in place.

Early versions of this app would frequently crash with a timeout exception.
It now has a mechanism in place to retry if it runs into a rate limit, but
as an administrator I'm not able to test this effectively.