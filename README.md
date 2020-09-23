﻿<div align="center">

## Previous/Next


</div>

### Description

This code will search trough an MySQL database and display the number of results as you want. You can say i want a limit of 25 results. If there are more results this script will print :

'Previous' 1,2,3,4,5,etc. 'Next'. I quarante you that this code works for 100%! If you want to see this code alive you can visit one of the sites i.ve made : http://www.yipee.nl, this site uses this code on several pages. If you like tjis code, please vote for me.
 
### More Info
 
Code returns the result of a MySQL database


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jor](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jor.md)
**Level**          |Intermediate
**User Rating**    |3.6 (25 globes from 7 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Databases](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/databases__8-5.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jor-previous-next__8-413/archive/master.zip)

### API Declarations

Free for use!


### Source Code

```
****************************************************************
****************************************************************
** This code will search trough records in an SQL database and**
** display the amount of results that you want. If there are **
** more records than the maximum amount it will display    **
** 'Previous 1,2,3,4,etc. 'Next'. This code works!!! If you  **
** want to see this code alive, you can visit one of the sites**
** we have made. www.yipee.nl uses this code on several pages **
** If you have any questions you can send me an email at the **
** following address : dorst@ddwebdesign.nl          **
**                              **
** Note : This code seems long and complicated but if you read**
** the comment carefully you'll see its actually very easy!  **
****************************************************************
****************************************************************
* = Not nessesary for this code to work, so you can delete this stuff if you want.
<?php
// Connect to SQL database
$global_db = mysql_connect('localhost', 'username', 'password');
mysql_select_db('databasename', $global_db);
// First query to find out how many records we have
$query = "SELECT Fields FROM Table WHERE your conditions";
$result = mysql_query($query);
// Number of records found
$num_record = mysql_num_rows($result);
// Number of records you want to display per page
$display = 25;
// Message when no records found
$XX = 'Sorry, no results were found!';
// If there are no records then startrow is 0
if (empty($startrow)) {
  $startrow=0;
}
// Actual query, watch the end of the query, here's where we set the LIMIT per page
$query2 = "SELECT Fields FROM Tabel WHERE your conditions LIMIT $startrow, $display";
$result2 = mysql_query($query2);
* Put the results in a table
print("<table border=0><tr>");
* I want only 3 results (in this case pictures) on 1 line, therefore i need a counter
$counter = 0;
// Fetch the results (Begin loop)
while(list($Fields) = mysql_fetch_array($result2)) {
* If we have one line of three, move to the next line
if ($counter == 3) {
print("</tr><tr>");
* Set the counter to zero
$counter = 0;
}
// Display the results on the screen, this is just an example, make your own tabel here
print("<td bgcolor=#004A80 width=200 height=200 align=center><font color=#FFFFFF>$Field1</font><br><a href=\"showdetail.php?ID=$id\"><img src=\"images/$Image\" border=0 width=170 height=170></a><br><font color=#FFFFFF>FL $PriceNlg&nbsp&nbsp&nbsp&#8364; $PriceEuro</font></td>");
* Increase the counter with 1
$counter = $counter + 1;
}
// End loop
// Calculate the previous results, only print 'Previous' if startrow is not equal to zero
if ($startrow != 0) {
  $prevrow = $startrow - $display;
  print("<a href=\"$PHP_SELF?startrow=$prevrow\">Previous</a>&nbsp"); \\ Of cource here you can send more
}                                     variables seperated by &
// Calculate the total number of pages
$pages = intval($num_record / $display);
// $pages now contains number of pages needed unless there are left over from division
if ($num_record % $display) {
	// has left over from division, so add one page
  $pages++;
}
// Print the next pages, first check if there are more pages then 1
if ($pages > 1) {
for ($i=1; $i <= $pages; $i++) { // Begin loop
  $nextrow = $display * ($i - 1);
  print("<a href=\"$PHP_SELF?startrow=$nextrow\">$i</a>&nbsp&nbsp"); \\ Also here you can send more
}                                     variables seperatd by &
}
//End loop
// Check if we are at the last page, if so, dont print 'Next'
if (!(($startrow / $display) == $pages) && $pages != 1) {
  // not the last page so print 'Next'
  $nextrow = $startrow + $display;
  print("<a href=\"$PHP_SELF?startrow=$nextrow\">Next</a>");
}
// If there are no results at all
if ($num_record < 1) {
print("<table border=0 width=795><tr><td>$XX</td></tr></table>");
}
?>
```

