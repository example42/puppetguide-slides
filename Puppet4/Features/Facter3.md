# Facter 3

Older versions of facter returned key - value pairs.

Facter 3 returns a structured hash of data and knows about differences like string, boolean and array.
With facter 3 it is no longer required to e.g. transform the string 'true' into a boolean value.

To get all results just run ```facter```

This will return the following (shortened output):

    disks => {
      sda => {
        model => "VBOX HARDDISK",
        size => "20.00 GiB",
        size_bytes => 21474836480,
        vendor => "ATA"
      }
    }
    processors => {
      count => 4,
      isa => "unknown",
      models => [
        "Intel(R) Core(TM) i7-3635QM CPU @ 2.40GHz",
        "Intel(R) Core(TM) i7-3635QM CPU @ 2.40GHz",
        "Intel(R) Core(TM) i7-3635QM CPU @ 2.40GHz",
        "Intel(R) Core(TM) i7-3635QM CPU @ 2.40GHz"
      ],
      physicalcount => 1
    }
