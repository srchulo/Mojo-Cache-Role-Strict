# NAME

Mojo::Cache::Role::Strict - Require that keys exist when getting cached values or throw

# STATUS

<div>
    <a href="https://travis-ci.org/srchulo/Mojo-Cache-Role-Strict"><img src="https://travis-ci.org/srchulo/Mojo-Cache-Role-Strict.svg?branch=master"></a>
</div>

# SYNOPSIS

    my $strict_cache = Mojo::Cache->new->with_roles('+Strict');

    $strict_cache->set(key_that_exists => 'I am here!');

    # prints "I am here!"
    say $strict_cache->get('key_that_exists');

    # dies
    say $strict_cache->get('nonexistent_key');

# DESCRIPTION

[Mojo::Cache::Role::Strict](https://metacpan.org/pod/Mojo::Cache::Role::Strict) is a role that makes your [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache) instance strict by
dying when keys that are provided to ["get" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#get) do not exist in the cache (have not
been set with ["set" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#set)).

# METHODS

## exists

    if ($cache->exists('key')) {
      ...
    }

Returns `true` if a cached value exists for the provided key, `false` otherwise.

["exists"](#exists) is composed from [Mojo::Cache::Role::Exists](https://metacpan.org/pod/Mojo::Cache::Role::Exists). See that module for more information.

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
