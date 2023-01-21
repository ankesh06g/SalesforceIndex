# Visualforce

## Where to use?

1. Email Template
2. Generate PDF
3. Custom Tabs
4. Record Pages
5. Override button funtionality

## <apex:page> Attributes

### 1. Action

- This method is called before the page is rendered, and allows you to optionally redirect the user to another page.
- If an action isn’t specified, the page loads as usual. If the action method returns null, the page simply refreshes.
- Do not use this action for initialization or DML.

### 2. standardController

The name of the Salesforce object that’s used to control the behavior of this page. This attribute can’t be specified if the controller attribute is also present.

### 3. Controller

The name of the **custom controller** class written in Apex used to control the behavior of this page. This attribute can’t be specified if the standardController attribute is also present.
To implement all of the logic for a page and bypass default Salesforce functionality

### 4. extensions

The name of one or more custom controller extensions written in Apex that add additional logic to this page.

### 5. renderAs

To make page to be render as PDF.

Other:

StandardSetController - for pagination in VF
