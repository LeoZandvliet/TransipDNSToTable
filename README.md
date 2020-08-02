# TransipDNSToTable

## TL;DR
Create a bookmark in your webbrowser with one of these pieces of javascript to transform the DNS Entries of a domain in your TransIP control panel to:
* [CSV text](https://raw.githubusercontent.com/LeoZandvliet/TransipDNSToTable/master/to-csv.txt)
* [Html table](https://raw.githubusercontent.com/LeoZandvliet/TransipDNSToTable/master/to-table.txt)
* [XML](https://raw.githubusercontent.com/LeoZandvliet/TransipDNSToTable/master/to-xml.txt)
* [RFC-1053](to-rfc1053.txt)

Then copy and paste the converted data to another program!

## Explanation
In the TransIP dashboard, the DNS entries of your domains are easy to edit,
and difficult to copy to another administration.

The table of DNS entries consists of div elements containing input and select elements:

    <div class="form-group">
	<div class="col-md-3 col-md-inline-form">
		<label class="visible-xs visible-sm">Naam</label>
		<input type="text" name="name[]" class="form-control input-sm name" value="@">
	</div>
	<div class="col-md-2 col-md-inline-form">
		<label class="visible-xs visible-sm">TTL</label>
		<select name="expire[]" class="form-control input-sm expire">
			<option value="86400" selected="">1 Dag</option>
		</select>
	</div>
	<div class="col-md-2 col-md-inline-form">
		<label class="visible-xs visible-sm">Type</label>
		<select name="type[]" class="form-control input-sm type">
			<option value="A" selected="">A</option>
		</select>
	</div>
	<div class="col-md-5 col-md-inline-form form-inline-delete-sm">
		<label class="visible-xs visible-sm">Waarde</label>
		<input type="text" name="content[]" class="form-control input-sm content" value="123.456.789.1">
	</div>
    </div>

This looks nice when displayed by the browser, but is terrible to copy to an spreadsheet program or most other programs that handle tables, csv or xml well.

Therefore I wrote several pieces of javascript that can be added as bookmark in Google Chrome, Firefox, Safari, etc to quickly convert the DNS entries to:

* [CSV text](to-csv.txt)
* [Html table](to-table.txt)
* [XML](to-xml.txt)
* [RFC-1053](to-rfc1053.txt)

**NOTE**: The RFC-1053 format can be used to import your records into a AWS Route 53 hosted zone.

Human readable versions are located in the [src directory](https://github.com/LeoZandvliet/TransipDNSToTable/blob/master/src/).

## Example output

### CSV

```
name;TTL;Type;Value
@;1 Dag;A;123.456.789.1
```

### Table 

| name | TTL | Type | Value |
| --- | --- | --- | --- |
| @	| 1 Dag | A | 123.456.789.1 |

### XML

```
<dnsEntries>
	<dnsEntry>
		<name>*</name>
		<ttl>1 Dag</ttl>
		<type>CNAME</type>
		<value>123.456.789.0</value>
	</dnsEntry>
</dnsEntries>
```

### RFC-1053

See [https://tools.ietf.org/html/rfc1035](https://tools.ietf.org/html/rfc1035).

```
$ORIGIN <DOMAIN>.
@ 1D IN A 123.456.789.1
```

## Script breakdown
1. Add jQuery to the page
2. Create a funtion txt() to retrieve the displayed texts from input or option label
3. Callback when jQuery is loaded:
   1. Iterate over the several `.form-group` to transform to table cells in a table row
   2. Inject the 'table' into the DOM and replace the html of `form.dns`.
4. The html can then be copied and pasted by the user's wishes.

## Resources
 * [Bookmarklets](http://caiorss.github.io/bookmarklets.html)
 * [Dynamically Load jQuery Library Using Plain JavaScript](https://www.sitepoint.com/dynamically-load-jquery-library-javascript/)
