# Start Different ECR Workflow Based on Product Line

This sample shows a way to start a different workflow based on the Product Line specified during creation of ECR item.

## History

This project and the following release notes have been migrated from the old Aras Projects page.

Release | Notes
--------|--------
[v2.0.0](https://github.com/ArasLabs/start-specific-workflow/releases/tag/v2.0.0) | Workflow Method Update. Tested on Aras 11.0 SP12 and SP15.
[v1](https://github.com/ArasLabs/start-specific-workflow/releases/tag/v1) | Initial Release

#### Supported Aras Versions

Project | Aras
--------|------
[v2.0.0](https://github.com/ArasLabs/start-specific-workflow/releases/tag/v2.0.0) | Aras 11.0 SP12+ 
[v1](https://github.com/ArasLabs/start-specific-workflow/releases/tag/v1) | Aras 9.2.0 SP3

## Installation

#### Important!
**Always back up your code tree and database before applying an import package or code tree patch!**

### Pre-requisites

1. Aras Innovator installed
2. Aras Package Import tool
3. **ProductLineBasedWorkflow** import package

### Install Steps

1. Backup your database and store the BAK file in a safe place.
2. Open up the Aras Package Import tool.
3. Enter your login credentials and click **Login**
    * _Note: You must login as root for the package import to succeed!_
4. Enter the package name in the TargetRelease field.
    * Optional: Enter a description in the Description field.
5. Enter the path to your local `..\ProductLineBasedWorkflow\Import\imports.mf` file in the Manifest File field.
6. Select all in the Available for Import field.
7. Select Type = **Merge** and Mode = **Thorough Mode**.
8. Click **Import** in the top left corner.
9. Close the Aras Package Import tool.
10.	Login to Aras as admin.
11. Navigate to **Administration > ItemTypes** in the TOC.
12. Search for the "ECR" ItemType and open for editing.
13. In the "Properties" tab of the ECR ItemType click **New Relationship icon** to create a new Property with the following specifics:
    - Label: Product Line
    - Name: product_line
    - Data Type: List
    - Data Source[…]: Product Line Workflow List (Note: This List is imported in step 1 above)
    - Required: checked
14. In the “Server Events” tab select **Pick Related** and click **New Relationship icon**. 
15. In the resulting Search Dialog, search and select **ProductLine Workflow Instantiate** Method(Note: This Method is imported in step 1 above).
16. In the Event column select **onAfterAdd** from the drop-down list.
17. In the Workflows tab add **ECR2** and **ECR3** Workflows. ECR Workflow should already be there. 
    - Note: Make sure NONE of the Workflows is selected as Default (uncheck all the Checkboxes).
18. Save, Unlock, and Close the ECR ItemType.
19. Navigate to **Administration > Forms** in the TOC.
20. Search for the ECR Form and open it for editing. 
21. Add the newly added Property (product_line) to the form and label the field “Product Line”.
22. Save, Unlock, and Close the ECR Form.

## Usage

1. Create an instance of “ECR” ItemType. 
2. Since the property represented by the field in the form labeled “Product Line” is Mandatory, select one of the options in the drop-down List. The selected option will determine the specific Workflow process that is started.

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request

## Credits

Created by Aras Corporation Support.

## License

Published to Github under the MIT license. See the [LICENSE file](./LICENSE.md) for license rights and limitations.
