# NAME

Bot::ChatBots::Trello - Trello adapter for Bot::ChatBots

# VERSION

This document describes Bot::ChatBots::Trello version {{\[ version \]}}.

<div>
    <a href="https://travis-ci.org/polettix/Bot-ChatBots-Trello">
    <img alt="Build Status" src="https://travis-ci.org/polettix/Bot-ChatBots-Trello.svg?branch=master">
    </a>
    <a href="https://www.perl.org/">
    <img alt="Perl Version" src="https://img.shields.io/badge/perl-5.10+-brightgreen.svg">
    </a>
    <a href="https://badge.fury.io/pl/Bot-ChatBots-Trello">
    <img alt="Current CPAN version" src="https://badge.fury.io/pl/Bot-ChatBots-Trello.svg">
    </a>
    <a href="http://cpants.cpanauthors.org/dist/Bot-ChatBots-Trello">
    <img alt="Kwalitee" src="http://cpants.cpanauthors.org/dist/Bot-ChatBots-Trello.png">
    </a>
    <a href="http://www.cpantesters.org/distro/B/Bot-ChatBots-Trello.html?distmat=1">
    <img alt="CPAN Testers" src="https://img.shields.io/badge/cpan-testers-blue.svg">
    </a>
    <a href="http://matrix.cpantesters.org/?dist=Bot-ChatBots-Trello">
    <img alt="CPAN Testers Matrix" src="https://img.shields.io/badge/matrix-@testers-blue.svg">
    </a>
</div>

# SYNOPSIS

    # A minimal Trello Bot using WebHooks
    use Mojolicious::Lite;
    plugin 'Bot::ChatBots::Trello' => instances => [
       [
          'WebHook',
          processor  => \&processor,
          url        => $ENV{URL}, # whatever you think is good
       ],
       # more can follow here...
    ];
    app->start;
    sub processor {
       my $record = shift;
       say $record->{payload}{action}{type} ' happened';
       return $record;
    }

# DESCRIPTION

This module allows you to to define [Bot::ChatBots](https://metacpan.org/pod/Bot::ChatBots) for
[Trello](https://trello.com/), a kanban boards online application.

Strictly speaking, this _module_ is a [Mojolicious](https://metacpan.org/pod/Mojolicious) plugin that allows
you to load and use [Bot::ChatBots::Telegram::WebHook](https://metacpan.org/pod/Bot::ChatBots::Telegram::WebHook) (see ["SYNOPSIS"](#synopsis)
for a quick example), providing a way to receive _actions_ from Trello.

These modules rely upon [Log::Any](https://metacpan.org/pod/Log::Any) for emitting logging information; you
are encouraged to read that module's documentation for further
information. For what we are concerned, you have to remember that all logs
will be lost unless you configure [Log::Any](https://metacpan.org/pod/Log::Any), e.g. to send messages on
standard output you can do this:

    use Log::Any::Adapter qw< Stderr >;

If using the web hook, then you will probably want to send the logs
together with [Mojolicious](https://metacpan.org/pod/Mojolicious)'s logs, like this:

    use Mojolicious::Lite;
    use Log::Any::Adapter;
    Log::Any::Adapter->set(MojoLog => logger => app->log);

The configuration above relies on the presence of
[Log::Any::Adapter::MojoLog](https://metacpan.org/pod/Log::Any::Adapter::MojoLog).

# METHODS

All the heavylifting is done by [Bot::ChatBots::MojoPlugin](https://metacpan.org/pod/Bot::ChatBots::MojoPlugin).

# BUGS AND LIMITATIONS

Report bugs either through GitHub (patches welcome).

# SEE ALSO

[Bot::ChatBots](https://metacpan.org/pod/Bot::ChatBots), [Bot::ChatBots::Trello::WebHook](https://metacpan.org/pod/Bot::ChatBots::Trello::WebHook).

# AUTHOR

Flavio Poletti <polettix@cpan.org>

# COPYRIGHT AND LICENSE

Copyright (C) 2018 by Flavio Poletti <polettix@cpan.org>

This module is free software. You can redistribute it and/or modify it
under the terms of the Artistic License 2.0.

This program is distributed in the hope that it will be useful, but
without any warranty; without even the implied warranty of
merchantability or fitness for a particular purpose.
