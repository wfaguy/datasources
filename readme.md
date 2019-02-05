# Overview

## UTF8 encoding

It's important to think ahead. If we look at some current WFA datasources, they tend to import and convert to "byte". This is a typical, we live in a English-only world. I'm from Belgium and we have characters like é and è. And what about Hebrew or Chinese. Sure every now and then one of those special characters slip in and the byte conversion will fail.

Use the following trick to add UTF8 embedded text to your WFA CSV-files.

```powershell
$Utf8NoBomEncoding = New-Object System.Text.UTF8Encoding $False

function addCsvUtf8($path,$text){
	$text | %{[System.IO.File]::AppendAllText((resolve-path $path), "$_`n",$Utf8NoBomEncoding)}
}

#Example :

addCsvUtf8 -path $mycsvpath -text "$id`t$name`t$anyfield"

```

## Vmware vcenter 6.5 fixed datasource for UTF8

Using the function above, this datasource is now adapted to import UTF8 characters, which can be anywhere (datastorenames for example).

## Excel datasource

Import and export excel files
