# Config::Simple

This is a simple module to offer you a simple interface for when you need a configuration file.
It support various format. The default file format is a perl6 expression.

It main use is for simple configuration file that work like the ini format.
It work like a %hash object with additionnal .read and .write method


## Dependancy and installation

The module depend on `Data::Dump` for the default format.

`Config::INI` for the the ini format

`JSON::Pretty`for JSON


## Example

```perl
my $conf = Config::Simple.new #Provide a default format
#my $conf = Config::Simple.new(:b('ini')) #if you want to use a ini file;
$conf.filename = "myconf.conf";

$conf<video><title> = "Dune"
$conf<subtitle><file> = "Dune_sub.ssa"
$conf<subtitle><format> = "ssa";

$conf.write(); # write the conf to a file
$conf.write("mycopyconf.con"); # you can also specify another file

# to read from an already existing file

$conf = Config::Simple.read("myconf.conf") # or .read("myconf.conf", :b("ini"))
say $conf<video><title>; #Dune

```

## Formats

For now, the only available formats are `ini` and `JSON` the case is important since it try to load the Config::Simple::<format> module.

For `ini` format provide a _ key for the root. `$conf<_><something>` to read stuff not put in a section

## Writting a new format module

Create a Config::Simple::myformat class that does Config::Simple::Role and define a `write` and `read` method

## TODO

Edit the format tests for skipping when the attached module is not installed