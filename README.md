# PowerApps_Collect-Large-SharePoint-List

## Solution Details
This solution can be used to pull more than 2000 records from a SharePoint list into a PowerApps collection. 

While this is typically not recommended, there are situations where it is needed.

## Solution Architecture
### SharePoint List
This solution is based around a SharePoint online list that has more than 2000 rows. 

Because the SharePoint ID column is not delegable in PowerApps using the >,>=, <, <= comparison operators, a new column must be created to store a copy of the list item ID as an integer so that PowerApps can delegate calls to the ID of the list item using the newly created column. In this solution, that column is called "ListID." This column should be indexed for improved performance. 

### Power Automate Flows
#### "Add ListID to SPO List Item When Created"
This is a Flow that will automatically populate the ListID column with the ID of each row (list item) that is created in the SharePoint list.

#### "Update ListID for all SPO List Items" (Optional)
This flow can be used to update the ListID for all existing rows in a SharePoint list where the ListID column did not previous exist. 

### PowerApp "Collect Large SPO Lists"
The PowerApp contains the formula that allows collection of more than 2000 rows of a SharePoint list. The formula is contained in the btnLoad_colAllRecords and will load all of the list items from a single list into a PowerApps collection called "colAllRecords"

## Solution Configuration

### SharePoint List
1. Create "ListID" column in SharePoint List
2. Index "ListID" column in SharePoint List

### PowerApps/Power Automate Solution
1. Import solution
2. Open each Power Automate flow in the solution  ("Add ListID to SPO List Item When Created" and "Update ListID for all SPO List Items") and perform the following tasks:
  1. Turn the Flow on (Flows are automatically turned off when importing a solution)
	2. Edit each flow
		1. Update connection reference for SharePoint connection
		2. Update all SharePoint triggers & actions to point to your large SharePoint List
3. Open the "Collect Large SPO Lists" PowerApp in Edit Mode and perform the following tasks:
  1. Connect the PowerApp to your large SPO List
  2. Open the "LoadLargeCollection Screen"
    1. Open the 'OnSelect' property of button "btnLoad_colAllRecords"
      1. Find and Replace all instances of 'Large SPO List' with the name of your large SPO list
    c. Select "btnLoad_colAllRecords" to test collecting all SPO list items into a collection called "colAllRecords".
