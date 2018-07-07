Sparse documentation:

```
Syntax:	  pcre_match (STR <subject>, STR <pattern> [, <case matters> 0] [, <repeat until no matches> 1]	=> LIST

The function `pcre_match()' searches <subject> for <pattern> using the Perl Compatible Regular Expressions library. The return value is a list of maps containing each match. Each returned map will have a key which corresponds to either a named capture group or the number of the capture group being matched. The full match is always found in the key "0". The value of each key will be another map containing the keys 'match' and 'position'. Match corresponds to the text that was matched and position will return the indices of the substring within <subject>.

If <repeat until no matches> is 1, the expression will continue to be evaluated until no further matches can be found or it exhausts the iteration limit. This defaults to 1.

Additionally, wizards can control how many iterations of the loop are possible by adding a property to $server_options. $server_options.pcre_match_max_iterations is the maximum number of loops allowed before giving up and allowing other tasks to proceed. CAUTION: It's recommended to keep this value fairly low. The default value is 1000. The minimum value is 100.

Examples:

Extract dates from a string:
pcre_match("09/12/1999 other random text 01/21/1952", "([0-9]{2})/([0-9]{2})/([0-9]{4})")
=> {["0" -> ["match" -> "09/12/1999", "position" -> {1, 10}], "1" -> ["match" -> "09", "position" -> {1, 2}], "2" -> ["match" -> "12", "position" -> {4, 5}], "3" -> ["match" -> "1999", "position" -> {7, 10}]], ["0" -> ["match" -> "01/21/1952", "position" -> {30, 39}], "1" -> ["match" -> "01", "position" -> {30, 31}], "2" -> ["match" -> "21", "position" -> {33, 34}], "3" -> ["match" -> "1952", "position" -> {36, 39}]]}

Explode a string (albeit a contrived example):
;;ret = {}; for x in (pcre_match("This is a string of words, with punctuation, that should be exploded. By space. --zippy--", "[a-zA-Z]+", 0, 1)) ret = {@ret, x["0"]["match"]}; endfor return ret;
=> {"This", "is", "a", "string", "of", "words", "with", "punctuation", "that", "should", "be", "exploded", "By", "space", "zippy"}
```
