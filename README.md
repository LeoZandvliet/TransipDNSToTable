# TransipDNSToTable

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

This looks nice when displayed by the browser, but is terrible to copy to an spreadsheet program or most other programs that handle tables well.

Therefore I wrote [this piece of javascript](bookmark-content.txt) that can be added as bookmark in Google Chrome, Firefox, etc by adding a bookmark with the contents of the file `bookmark-content.txt`.

Script breakdown:
1. Add jQuery to the page
2. Create a funtion txt() to retrieve the displayed texts from input or option label
3. Callback when jQuery is loaded:
  1. Iterate over the several `.form-group` to transform to table cells in a table row
  2. Inject the 'table' into the DOM and replace the html of `form.dns`.
4. The html can then be copied and pasted by the user's wishes.
