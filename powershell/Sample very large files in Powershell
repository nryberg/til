# Sample very large file in Powershell	

Processing small files in Powershell is pretty fast and effective.  However if you're dealing with very large GB sized files, you can get stuck waiting for it to process. 

Use the -Tail flag with the number of records in get-content:

```powershell
$file = "C:\Users\nick\Dropbox\Develop\Data\Flights\Historical\flightlist_20200101_20200131.csv"

$sample = "C:\Users\nick\Dropbox\Develop\Data\Flights\Historical\sample.csv"

gc -Path $file -Tail 100 | Out-File $sample -Encoding ascii

```