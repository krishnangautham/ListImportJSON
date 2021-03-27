# ListImportJSON
Imports a list of JSON feed and returns the results to be inserted into a Google Spreadsheet. ListImportJSON.gs adds a =ListImportJSON() function to your spreadsheet, allowing quick and easy JSON importing. To use go to Tools > Script Editor and add the ListImportJSON.gs file. Now in your spreadsheet you can access the ListImportJSON() function.

The JSON feed is flattened to create a two-dimensional array. For every JSON feed in the list, the first row contains the headers, with each column header indicating the path to that data in the JSON feed. The remaining rows contain the data.

By default, data gets transformed so it looks more like a normal data import. Specifically:

Data from parent JSON elements gets inherited to their child elements, so rows representing child elements contain the values of the rows representing their parent elements.
Values longer than 256 characters get truncated.
Headers have slashes converted to spaces, common prefixes removed and the resulting text converted to title case.
To change this behavior, pass in one of these values in the options parameter:

    noInherit:     Don't inherit values from parent elements
    noTruncate:    Don't truncate values
    rawHeaders:    Don't prettify headers
    noHeaders:     Don't include headers, only the data
    allHeaders:    Include all headers from the query parameter in the order they are listed
    debugLocation: Prepend each value with the row & column it belongs in
Example:

=ListImportJSON("ebiSearchList",1,50,6 "/version, /Resultlist/Result",
            "noInherit,noTruncate")


    @param {sourceSheet}        Source Sheet name from whil urls need to be fetched.
    @param {fromRow}            Row number from which url to be picked from sourceSheet.
    @param {toRow}              Row number upto which url to be picked.
    @param {queryColumnNumber}  Column number of sourceSheet where urls are available.
    @param {query}        a comma-separated list of paths to import. Any path starting with one of these paths gets imported.
    @param {parseOptions} a comma-separated list of options that alter processing of the data
    @customfunction
    
Review ListImportJSON.gs for more info on how to use these in detail. Script developers can easily extend the functionality of this library by using ImportJSONAdvanced function. An example spreadsheet is also attached.
