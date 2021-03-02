# Tips for fixing frontend in Data Engine

Data Engine Frontend is mainly localized in the **data-engine-taglib**. Inside this directory, there are 2 divisions:

- Data\_layout\_builder
  - Responsible for the creation of definitions. Depending on the project using the DE Taglib, can be: creation of _Structures_ (ECHO) or _Doc Types_ (Lima).
  - See more information [here](https://docs.google.com/document/d/1ZBFJm88d-FmQhhzKeGScZWP-wVvKHcCE8XFkfLpfr5E/edit).
- Data\_layout\_renderer
  - Responsible for the visualization of definitions and allows the input of values. Depending on the project using the DE Taglib, can be: creation of _Web Content_ (ECHO) or _Docs and Media_ (Lima).
  - See more information [here](https://docs.google.com/document/d/1BYAS4U0-apIjb1dBTn1UWnwFwm3_mAUXJGI6Dtuz4_g/edit).

Besides data-engine-taglib, Data Engine uses the frontend of Forms project.

Example:

- dynamic-data-mapping-form-builder
- dynamic-data-mapping-form-field-type
- dynamic-data-mapping-form-renderer

**Builder Taglib:**

- Uses the classes inside _data\_layout\_builder_
- Uses the classes inside _dynamic-data-mapping-form-builde_r, _dynamic-data-mapping-form-field-type_

On _dynamic-data-mapping-form-field-type_, you can reach every one of the fields. This module specifies how they are implemented.

Every field has its own properties, like: Label, Help Text, Placeholder. All these properties are represented by one field, example: the property label of a field is represented by a text field in the sidebar (i.e. [every setting of a field is a field itself](https://github.com/liferay/liferay-portal/blob/master/modules/apps/dynamic-data-mapping/dynamic-data-mapping-api/src/main/java/com/liferay/dynamic/data/mapping/form/field/type/DDMFormFieldTypeSettings.java))

![](RackMultipart20210302-4-vxmn2z_html_b46eb73b8f8ff1ee.png)

Saying that, if you are having a problem related to the value of a property (e.g. not persisting for any reason), **you should investigate the settings context of the field** :

![](RackMultipart20210302-4-vxmn2z_html_9fb6073c98038489.png)

While debugging the frontend, this property _settingsContext_ follow the same structure of the tabs in the field&#39;s sidebar:

![](RackMultipart20210302-4-vxmn2z_html_5e3502ff4734514e.png)

Each page has a specific group of properties:

![](RackMultipart20210302-4-vxmn2z_html_119441e62e22e4ba.png)

**DataLayoutBuider.es.js** is responsible for initializing the sidebar and form layout besides dispatching the language change action.

For each event you dispatch within the builder, probably you&#39;ll have a file called field$**[event\_name]**Handler.es.js that handles that event. For instance:

- es.js
- es.js
- es.js
- es.js

All these files are called by LayoutProvider.es.js

**Files:**

- es.js
  - Responsible for handling events like removing, duplicating, focusing and blurring fields

- es.js
  - Responsible for generic behaviors of the fields, like repeatable, readOnly, required, etc

eWE

- es.js
  - Initializes the DE Builder settings sidebar. There, events like double click and single click are attributed

- es.js
  - Where the settings context from a given field type is loaded.

- es.js
  - Lists the fieldsets in the sidebar and opens the fieldset modal in order to edit a fieldset

- useCreateFieldSet
  - Responsible to create and save a fieldset by using the modal.
  - End of the frontend&#39;s line before the request to save the fieldset.

- useSaveFieldSet
  - Responsible for editing an existing fieldset by using the modal.
  - End of the frontend&#39;s line before the request to edit an existing fieldset.

- es.js
  - End of the frontend&#39;s line before the request to save the data definition is made.

**Renderer Taglib:**

- Uses the classes inside _data\_layout\_renderer_
- Uses the classes inside _dynamic-data-mapping-form-renderer_

**Files:**

- es.js
  - Form root component
  - It initializes pageLanguageUpdate.es.js
- es.js (ddm-...)
  - Every time you change the language it passes through here
  - Also during the first load of the page.
- es.js
  - Every time you change the language, this file sets the value based on the localizedValue
- es.js
  - It passes through this file when you changed a field value
- es.js
  - Responsible for handling events like removing, duplicating, focusing and blurring fields