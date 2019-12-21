# NAME

Mojo::Cache::Role::Strict - Limit get to keys that exist and prevent calls to set

# STATUS

<div>
    <a href="https://travis-ci.org/srchulo/Mojo-Cache-Role-Strict"><img src="https://travis-ci.org/srchulo/Mojo-Cache-Role-Strict.svg?branch=master"></a> <a href='https://coveralls.io/github/srchulo/Mojo-Cache-Role-Strict?branch=master'><img src='https://coveralls.io/repos/github/srchulo/Mojo-Cache-Role-Strict/badge.svg?branch=master' alt='Coverage Status' /></a>
</div>

# SYNOPSIS

    my $strict_cache = Mojo::Cache->new
                                  ->set(key_that_exists => 'I am here!')
                                  ->with_roles('+Strict')
                                  ;

    # prints "I am here!"
    say $strict_cache->get('key_that_exists');

    # get key that doesn't exist dies
    say $strict_cache->get('nonexistent_key');

    # setting new key dies
    $strict_cache->set(new_key => 'I die!');

    # updating existing key dies
    $strict_cache->set(key_that_exists => 'I die!');

    # allow nonexistent keys to be passed to get
    my $value = $strict_cache->strict_get(0)->get('nonexistent_key');

    # allow keys to be set
    $strict_cache->strict_set(0)->set(new_key => 'I live!');

# DESCRIPTION

[Mojo::Cache::Role::Strict](https://metacpan.org/pod/Mojo::Cache::Role::Strict) is a role that makes your [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache) instance strict by
dying when calling ["get" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#get) with keys that do not exist in the cache (have not
been set with ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set)) and by dying when you call ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set). You can optionally
allow ["get" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#get) and ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set) with ["strict\_get"](#strict_get) and ["strict\_set"](#strict_set).

# METHODS

## exists

    if ($strict_cache->exists('key')) {
      my $value = $strict_cache->get('key');
      ...
    }

Returns `true` if a cached value exists for the provided key, `false` otherwise.

["exists"](#exists) is composed from [Mojo::Cache::Role::Exists](https://metacpan.org/pod/Mojo::Cache::Role::Exists). See that module for more information.

## strict\_get

    my $strict_cache = Mojo::Cache->new->with_roles('+Strict')->strict_get(0);

    # lives even though key does not exist
    my $value = $strict_cache->get('nonexistent_key');

["strict\_get"](#strict_get) specifies whether keys must exist when calling ["get" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#get). If `true`,
keys that do not exist will throw. If `false`, `undef` will be returned.

The default is `true`.

This method returns the [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache) object.

## strict\_set

    my $strict_cache = Mojo::Cache->new
                                  ->set(key_that_exists => 'I am here!')
                                  ->with_roles('+Strict')
                                  ->strict_set(0)
                                  ;

    # setting new key lives
    $strict_cache->set(new_key => 'I live!');

    # updating existing key lives
    $strict_cache->set(key_that_exists => 'new value');

["strict\_set"](#strict_set) specifies whether ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set) may be called. If `true`,
calling ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set) will throw. If `false`, calls to ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set) are allowed.

The default is `true`.

This method returns the [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache) object.

# AUTHOR

Adam Hopkins <srchulo@cpan.org>

# COPYRIGHT

Copyright 2019- Adam Hopkins

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO

- [Mojolicious](https://metacpan.org/pod/Mojolicious)
- [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache)
- [Mojo::Cache::Role::Exists](https://metacpan.org/pod/Mojo::Cache::Role::Exists)
