param($scanFolder, [String[]]$exclude)

if ([string]::IsNullOrEmpty($scanFolder)){
    $scanFolder="C:\GitSource"
}

if ($exclude.Length -eq 0){
    $exclude=@("node_modules","packages")
}

function Is-Deletable{
    param($exclude,$fullName)
    $result=1
    foreach($x in $exclude){
        if ($fullName.Contains($x)){
            $result=0
        }
    }

    return $result
}


Get-ChildItem $scanFolder -Include bin,obj -Recurse | 
    foreach($_) { 
        $deletable=Is-Deletable $exclude $_.FullName
        if ($deletable -eq 1){
             Write-Host $"{$_}"
             Remove-Item $_.FullName -Force -Recurse
        }
        
    }

