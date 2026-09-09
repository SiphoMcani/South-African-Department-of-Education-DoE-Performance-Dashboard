let   
    Source = Csv.Document(
        Web.Contents("https://witscloud-my.sharepoint.com/personal/1928856_students_wits_ac_za/Documents/Apps/Microsoft Power Query/Uploaded Files/DoE_Dataset1.csv"), 
        [Delimiter = ",", Columns = 9, Encoding = 65001, QuoteStyle = QuoteStyle.None]
    ),   
    #"Promoted headers" = Table.PromoteHeaders(Source, [PromoteAllScalars = true]),   
    #"Filtered rows" = Table.SelectRows(#"Promoted headers", each [District] <> null and [District] <> ""),   
    #"Trimmed text" = Table.TransformColumns(#"Filtered rows", {{"District", each Text.Trim(_), type nullable text}}),   
    #"Changed column type" = Table.TransformColumnTypes(#"Trimmed text", {
        {"Province", type text}, 
        {"Number of Enrollment", Int64.Type}, 
        {"Number of Male", Int64.Type}, 
        {"Number of Female", type text}, 
        {"Number Wrote", Int64.Type}, 
        {"Number Passed", Int64.Type}, 
        {"Number Failed", Int64.Type}, 
        {" Number Passed with Bachelors ", Int64.Type}
    }, "en-GB"),   
    #"Replaced value" = Table.ReplaceValue(#"Changed column type", "Limpoo", "Limpopo", Replacer.ReplaceText, {"Province"}),   
    #"Replaced value 1" = Table.ReplaceValue(#"Replaced value", "Lipopo", "Limpopo", Replacer.ReplaceText, {"Province"}),   
    #"Replaced value 2" = Table.ReplaceValue(#"Replaced value 1", "Mpmalanga", "Mpumalanga", Replacer.ReplaceText, {"Province"}),   
    #"Replaced value 3" = Table.ReplaceValue(#"Replaced value 2", "Mpumallnga", "Mpumalanga", Replacer.ReplaceText, {"Province"}),   
    #"Replaced value 4" = Table.ReplaceValue(#"Replaced value 3", "NorthWest", "North West", Replacer.ReplaceText, {"Province"}),   
    #"Replaced value 5" = Table.ReplaceValue(#"Replaced value 4", " ", "", Replacer.ReplaceText, {"Number of Female"}),   
    #"Changed column type 1" = Table.TransformColumnTypes(#"Replaced value 5", {{"Number of Female", Int64.Type}}),   
    #"Renamed columns" = Table.RenameColumns(#"Changed column type 1", {{" Number Passed with Bachelors ", "Number Passed with Bachelors"}})
