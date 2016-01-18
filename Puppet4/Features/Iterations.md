# Iterations

Puppet now supports iterations over resources. They are based on **lambdas**.

New functions, based on lambdas:

  - each, iterate over an array

        each (loop over arrays and hashes) $a = [ 1,2,3]
        each($a) | $value | { 
          notice $value 
        }
        $h = { '1' => ['a','b','c'], '2' => 'foo' }
        each($h) | $key, $value | { 
          notice "$key = $value"
        }

  - slice

  - filter

  - map

  - reduce

  - with
