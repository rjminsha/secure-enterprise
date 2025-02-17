---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-29"

keywords: onboard, catalog management, private catalog, catalog manifest, software, automation, metadata

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}

# Locally editing the catalog manifest
{: #manifest-values}

The catalog manifest file specifies the information about your onboarded software that you want to share with potential users through the catalog. You can provide licensing and compliance information, make specific settings, and provide descriptions about the intended purpose of your product.

Prefer to use the console to edit your catalog settings? You can make the selections by following the [provided wizard and then export the manifest file](/docs/secure-enterprise?topic=secure-enterprise-onboard-da).
{: tip}

## Editing your manifest
{: #edit-manifest}

To edit your manifest locally, you can use the following steps.

1. Copy the following example manifest file into a local editor.
2. Name the file `ibm_catalog.json`.
3. Add your preferred configurations into the file by using the example manifest as a guide. To learn more about each value, view the [available values](#available-values).
4. Add the file into the root folder of your source code repository.
5. [Add your deployable architecture to your catalog](/docs/secure-enterprise?topic=secure-enterprise-onboard-da-catalog).

## Example manifest file
{: #example-manifest}

The following code snippet can be used as a template.

```json
{
   "products": [
      {
         "name": "",
         "label": "",
         "product_kind": "",
         "tags": [
            "tag 1",
            "tag 2"
         ],
         "keywords": [
            "keyword 1",
            "keyword 2",
            "keyword 3"
         ],
         "short_description": "Short description of your product.",
         "long_description": "A longer description of your product.",
         "offering_docs_url": "URL",
         "offering_icon_url": "URL or emebbed image",
         "provider_name": "Community",
         "module_info": {
            "works_with": [
               {
                  "catalog_id": "",
                  "name": "module name",
                  "kind": "terraform",
                  "version": "0.1.0",
                  "flavor": "Variation name"
               }
            ]
         },
         "support_details": "Explanation of support.",
         "features": [
            {
               "title": "Feature 1 title"
               "description": "Feature 1 description"
            },
            {
               "title": "Feature 2 title"
               "description": "Feature 2 description"
            }
         ],
         "flavors": [
            {
               "label": "Display name",
               "name": "Programatic name",
               "install_type": "Install type",
               "working_directory": "Directory path",
               "usage_template": "template",
               "scripts": [
                  {
                     "type": "ansible",
                     "short_description": "Short description of what your script is intended to do.",
                     "path": "Path to script location.",
                     "stage": "The stage. For example, pre.",
                     "action": "The action. For example, validate."
                  }
               ],
               "change_notices": {
                  "breaking": [
                     {
                        "title": "Title of breaking change",
                        "description": "Description of the change."
                     }
                  ],
                  "new": [
                     {
                        "title": "Title of new feature",
                        "description": "Description of the new feature or capability."
                     }
                  ],
                  "update": [
                     {
                        "title": "Title of general update",
                        "description": "Description of the general update."
                     }
                  ]
               },
               "compliance": {
                  "authority": "scc-v3",
                  "controls": [
                     {
                        "profile": {
                           "name": "Security and Compliance Center profile name",
                           "version": "Profile version"
                        },
                        "names": [
                           "Control name 1 e.g. AC-2(a)",
                           "Control name 2",
                           "Control name 3"
                        ]
                     }
                  ]
               },
               "configuration": [
                  {
                     "key": "key type e.g. ssh_key",
                     "required": true
                  },
                  {
                     "key": "Key type e.g. ibmcloud_api_key",
                     "required": true,
                     "type": "The data type"
                  }
               ],
               "outputs": [
                  {
                     "description": "Output description",
                     "key": "key"
                  },
                  {
                     "description": "Output description",
                     "key": "key"
                  }
               ],
               "dependencies": [
                  {
                     "catalog_id": "",
                     "id": "",
                     "name": "",
                     "version": "",
                     "flavors": [
                        "Variation name 1",
                        "Variation name 2",
                        "Variation name 3"
                     ],
                     "install_type": "full stack or extension",
                  }
               ],
               "iam_permissions" [
                  {
                     "role_crns": [
                        "CRN 1 e.g. crn:v1:bluemix:public:iam::::serviceRole:Manager",
                        "CRN 2 e.g. crn:v1:bluemix:public:iam::::role:Administrator"
                     ],
                     "service_name": "Programatic service name e.g. is.vpc"
                  }
               ],
               "licenses": [
                  {
                     "name": "License name",
                     "smref": "Link to the license"
                  }
               ],
               "schematics_env_values": {
                  "value": "value",
                  "smref": "BRIAN WHAT IS THIS?"
               },
               "architecture": {
                  "descriptions": "BRIAN - WHAT IS THIS?",
                  "features": [
                     {
                        "title": "Feature 1 title",
                        "description": "Feature 1 description"
                     },
                     {
                        "title": "Feature 1 title",
                        "description": "Feature 1 description"
                     }
                  ],
                  "diagram": {
                     "caption": "Diagram caption",
                     "url": "Link to diagram or embedded image",
                     "metadata": []
                  },
                  "description": "Description of the diagram"
               }
            }
         ]
      }
   ]
}
```
{: codeblock}

## Available values
{: #available-values}

The following sections include information about each value that can be referenced in your manifest file.

### Products
{: #value-products}

The products value indicates an array of products with size one or more. If a catalog manifest file exists at the root of your repository, only the products within the file can be imported. Products are imported one at a time. The following values can be included at the `products` level:

`label`
:   The product display name. This value must match the display name that you provide during onboarding.

`name`
:   The programmatic name of the product.

`version`
:   The version of the product in SemVer format, including the major version, minor version, and revision, for example, 1.0.0. This value can also be specified when the product is onboarded to a catalog.

`product_kind`
:   The kind of product that you are onboarding. Valid values are software, module, or solution. A solution is otherwise known as a deployable architecture.

`tags`
:   An array of predefined values that can help users to filter the catalog to identify and learn more about your product.

`keywords`
:   An array of specific words or phrases that a user might try to search for.

`short_description`
:   A concise summary of what your product is and its value.

`long_description`
:   A detailed description of your product that explains the product's value and benefits to users.

`provider_name`
:   Users can filter the catalog by the provider of a product. When you onboard a product to a private catalog, the provider name is set to `Community` by default. However, you can customize this field to display your company or organization name. IBM is a reserved value and can be used for IBM build products only.

`offering_docs_url`
:   A link to documentation about the product that users can access.

`offering_icon_url`
:   A link to the URL where icon that you want to appear on the product's catalog entry page is located.

`support_details`
:   Support information in markdown format that can include support contacts, support locations, and support methods.

`features`
:   Section header for details that highlight the processes, abilities, and results of the product. These product-level features are listed on your catalog entry page with your product description. For example, features might incluce CPU requirements, security features, or more. Each entry is defined as an array as shown in the example manifest in the previous section.

   `title`
   :   The name of the feature.

   `description`
   :   A concise description of the feature.



### Modules
{: #value-module}

The `module_info` value indicates information about other products that the deployable architecture is compatible with. The following values can be included at the `module_info` level:

`works_with`
:   Section header for information about a singular product that is compatible with the deployable architecture.

   `catalog_id` (optional)
   :   ID of the catalog that houses the product. If not specified, the {{site.data.keyword.cloud_notm}} catalog is the default.

   `id` (optional)
	:   ID of the product. The ID is not required if the `name` value is set.

   `name` (optional)
	:   Programmatic name of the product that works with the deployable architecture.

   `kind`
	:   The format of the module that works with your deployable architecture. Most often this is `terraform`.

   `version`
	:   Version or range of product versions that work with the deployable architecture in SemVer format.

   `flavors` (optional)
	:   The programmatic names of the compatible variations. Variations are onboarded individually to a catalog and are given a version number. An example variation name might be `standard` or `advanced`.


### Flavors
{: #value-variations}

Section header for information about the deployable architecture variations. Flavors are now known as variations in the console. The following values can be included at the `flavors` level:

`label`
:   Variation display name.

`name`
:   Variation programmatic name.

`working_directory`
:   For a working directory that is at the root level of your repo, you don't need to specify the working directory. If it is not at the root, then list the path from the root of your repository. For example, `./examples/`.

`usage`
:   Information on how to embed the architecture or run it locally through Terraform.

`usage_template`
:   Similar to `usage`. With a template you can use variables as a place holder where the values can be substituted. The string is stored in the `usage` property.

    | Template variable | Replacement value |
    |:------------------|:------------------|
    | ${{version}} | The version string of this variation or flavor. |
    | ${{flavor}} | The programtic name of the variation or flavor. |
    | ${{kind}} | The implementation kind. I.e. `terraform`. |
    | ${{id}} | The offering or product ID. |
    | ${{name}} | The programatic name of the offering or product. |
    | ${{catalogID}} | The ID of the catalog where the offering or product is located. |
    | ${{workingDirectory}} | The working directory of the flavor or variation. |
    {: caption=" Table 1. Usage template values and descriptions" caption-side="bottom"}

`licenses`
:   Information about the end user license agreements that users are required to accept when they install the product. The license agreements are in addition to the {{site.data.keyword.cloud_notm}} Services Agreement.

	```json
	{
		"id": "string, license id",
		"name": "string, license display name",
		"type": "string, type of license, e.g. Apache xxx",
		"url": "string, URL for the license text",
		"description": "string, license description"
	}
	```
	{: screen} 

   `id`
	:   The license ID.

   `name`
	:   The name of the license.

   `type`
	:   The type of license. For example, Apache.

   `url`
	:   A URL to where the user can access the license agreement.

   `description`
	:   A description of the license.


`compliance`
:   Section header that indicates which compliance controls that the architecture satisfies with the default installation settings. The evaluation and validation of the claims made is completed by {{site.data.keyword.compliance_full}}.

	```json
	"compliance": {
		"authority": "scc-v3",
		"profiles": [
			{
					"profile_name": "",
					"profile_version": ""
			}
		]
	}
	```
	{: codeblock}

	You can list multiple profiles in your catalog manifest JSON file, but note that only the first profile is added to your compliance information in a private catalog.
	{: important}

   `authority`
	:   IBM Cloud Security and Compliance Center v3 is the only authority accepted. This is programatically written as `scc-v3`.

   `profiles`
	:   Section header that indicates the profile that contains the controls that are being claimed. You can view predefined profiles in {{site.data.keyword.compliance_short}}.

      `profile_name`
      :   The name of the profile. For example, `NIST`. You can find the profile name in {{site.data.keyword.compliance_short}}.

      `profile_version`
      :   The version of the profile. For example, `1.0.0`. You can find the profile name in {{site.data.keyword.compliance_short}}.

   `controls`
	:   Section header that indicates that the variation has claimed controls. The catalog manifest accepts an array of controls that you can claim on your variation by specifying a control's `profile_name`, `profile_version`, and `control_name`. You can view predefined profiles in {{site.data.keyword.compliance_short}}.

      `profile`
      :    Section header that indicates that you are adding controls from a specific profile.

         `name`
         :   The profile name of the claimed control. For example, `NIST`. You can find the profile name in {{site.data.keyword.compliance_short}}.

         `version`
         :   The version of the profile. For example, `1.0.0`. You can find the profile name in {{site.data.keyword.compliance_short}}.

      `names`
      :   Section header to indicate a list of claimed controls. For example:

      ```text
		"names": [
			"CM-7(b)",
			"AC-2(a)"
		]
      ```
      {: codeblock}
		
   If you have included controls in your readme and your catalog manifest file, the manifest file takes precedence. It is best practice to make sure the controls listed in your catalog manifest file match the controls in your readme file.
   {: note}


`change_notices` (optional)
:   A list of the three types of changes that you might want to alert your users to when releasing a new version of your deployable architecture. You can specify `breaking changes`, `new features`, and `general updates`. Breaking changes are those updates that break functionality that was available through a previous version. New features highlight any new functionality that a user might encounter with the new version. Updates encompass any changes that you want to highlight to a user such as a modified behavior that doesn't neccessarily break existing functionality or changes that make the deployable architecture easier for them to use.

	```json
	"change_notices": {
		"breaking": [
			{
				"title": "",
				"description": ""
			}
		],
		"new_features": [
			{
				"title": "",
				"description": ""
			}
		],
		"updates": [
			{
				"title": "",
				"description": ""
			}
		]
	}
	```
	{: codeblock}


`iam_permissions`(optional)
:   Section header for a list of all IAM permissions that are required for a user to work with your deployable architecture version. IAM permission information includes the programmatic name of the service that is required and a list of CRNs for roles that are needed. If you build your catalog manifest file from the UI, the CRNs are already included.


	```
	{
		"service_name": "IAM defined service name",
		"role_crns" [
			""
		],
		"resources": [
			{
				"name": "",
				"description": "",
				"role_crns: [
					""
				]
			}
		]
	}
	```
	{: codeblock}

   `service_name`
	:   The programmatic name of the service that users must have access to.

   `role_crns`
	:   Section header to indicate a list of access roles. For example:

   `resources`
	:   The resources for a permission.

      `name`
      :   The name of the resource.

      `description`
      :   A description of the resource.

      `role_crns`
      :   Section header to indicate a list of access roles. For example:

`architecture`
:   High-level information about the deployable architecture version that includes a description, features, and a diagram. Multiple diagrams, with captions, can be provided.

	```json
	"architecture" {
		"descriptions": "",
		"features": [
			{
				"title": "",
				"description": ""
			}
		],
		"diagrams": [
			{
				"diagram" {
					"caption": "",
					"url": "",
					"type": "image/svg+xml"
				},
				"description": ""
			}
		]
	}
	```
	{: codeblock}

   `features`
	:   Information that highlights the processes, abilities, and results of the version, or if applicable, architecture variation. When onboarding using the console, these details are called highlights. These details appear on the variation selection box within your catalog entry. If your product has multiple architecture variations, users can compare the variation-level features to decide which variation suits their needs.

      `title`
      :   Name of the feature.

      `description`
      :   A description of the feature.

   `diagrams`
	:   Information about the architecture diagram that includes the diagram caption, the URL to embed the SVG of the diagram, the diagram metadata such as element ID and element description, and the description of the reference architecture.

      `diagram`
      :   Section marker for information about a singular architecture diagram.

         `url`
         :   The URL to the diagram's SVG. You can also embed an SVG.

         `api_url`
         :   The catalog management API URL to the diagram.

         `url_proxy`
         :   Section header for information about a proxied image.

               `url`
               :   The URL to the proxied image.

               `sha`
               :   The `sha` indientifier of the image.
         
         `caption`
         A short label for the architecture diagram.

         `type`
         :   The type of media.

         `thumbnail_url`
         :   A link to a thumbnail for the diagram.

      `description`
      :   Information about architecture diagram as a whole, including the outline of the system and the relationships, constraints, and boundaries between components of the deployable architecture.

`dependencies`
:   Section header for a list of prerequisite products that are required to deploy the architecture. Information includes the programmatic name of the product and product versions. Optionally, you can include the catalog ID and a list of dependent variations.

	```json
	{
		"name": "offering name",
		"id": "offering ID",
		"kind": "terraform",
		"version": "SemVer version e.g. 3.1.2"
		"flavors": [
			"flavor name"
		],
		"install_type": "fullstack or extension",
		"catalog_id": "catalog ID"
	}
	```
	{: codeblock}

   `catalog_id` (optional)
	:   ID of the catalog that houses the product. If not specified, the {{site.data.keyword.cloud_notm}} catalog is the default.

   `id` (optional)
	:   The product ID. The ID is not required if the `name` value is set.

   `name` (optional)
	:   Programmatic name of the product.

   `kind`
	:   The format kind of the dependency.

   `version`
	:   A version or range of versions to include as dependencies in SemVer format.

   `flavors` (optional)
	:   List of variations that the architecture depends on.

`release_notes_url`
:   URL to the architecture's release notes.

`configuration`
:   Section header for that specifies the configuration of deployment variables for specific variation. Catalog data types are used to extend native types and faciliate for a better user experience when you're working in the IBM Cloud console. If you are running your code on a local machine or another environment, the variables are not used. An example might be a catalog type of `password` that is used to extend the capabilities of a Terraform variable defined with a type of `string` so that it is treated as sensitive in the UI.

```json
{
   "key": "The configuration key. This value should match the name of a deployment variable.",
   "type": "The data type of the variable. This must be a valid catalog management type.",
   "default_value": "The default value set by the person who onboarded the deployable architecture",
   "value_constraint": "string",
   "description": "The description of the variable that is shown in the catalog to those who use your deployable architecture.",
   "display_name": "The display name for the configuration type.",
   "required": boolean,
   "options": [
      "Selectable option 1",
      "Selectable option 2"
   ],
   "hidden": boolean,
   "custom_config": {
      "type": "The ID of the widget type.",
      "grouping": "Where the configuration type is rendered.",
      "original_grouping": "The original groupiing type for the configuration.",
      "grouping_index": "The order in which the configuration item shows in a particular grouping.",
      "config_constraints": "Map of constraint parameters that are passed to the custom widget.",
      "associations": "The list of parameters associated with the configuration.",
      "options_url": "The URL where the options for your custom type can be pulled by using dynamic data from objects in the catalog."
   },
   "configuration_group": "The name of the assocated configuration group."
}
```
{: codeblock}

   `key`
   :   The configuration key. The value should match the name of a deployment variable.

   `type`
   :   The type of input. The data type must be supported by the Catalog Management service. Native Terraform types map to one of the supported types. For example, the Terraform type `map` equates to `object`. The Terraform type `list` equates to `array`. A Terraform type `string` with a sensitive attribute, equates to `password`.

      Supported predefined types:
      * `boolean`
      * `float`
      * `int`
      * `number`
      * `password`
      * `string`
      * `object`

      Supported custom types:
      * `array`
      * `region`
      * `textarea`
      * `vpc`
      * `vpc ssh key`
      * `vpc region`
      * `cluster`
      * `power iaas`
      * `resource group`
      * `multi-line secure value`
      * `schematics workspace`
      * `json editor`
      * `preset configuration`

   `default_value`
   :   The value that is to be set as the default.


   `value_constraint`
   :   WHAT IS THIS?


   `description`
   :   A description of the variable that you want to display in the UI for users of your deployable architecture.
   
   `display_name`
   :   The name that is displayed for the configuration type.

   `required`
   :   A boolean that indicates if users are required to specify the parameter during installation.

   `hidden`
   :   A boolean that indicates if the parameter should be hidden from users during installation.

   `options`
   :   An array of options that users can choose from for a parameter.

   `custom_config`
   :   Section header use to indicate that a custom configuration can be used.

      `type`
      :   The ID of the widget type used for configuration

      `grouping`
      :   Where the configuration type should appear in the catalog. Valid values are `Target`, `Resource`, and `Deployment`.

      `original_grouping`
      :   Where the configuration type originally appeared. Valid values are `Target`, `Resource`, and `Deployment`.

      `grouping_index`
      :   The order of this configuration item when there are mulitple.

      `config_constraints`
      :   Map of constraint parameters that are given to the custom widget.

      `associations`
      :   Section header for parameters that are associated with the configuration.

   `configuration_group`
   :   The name of an associated configuration group.

`schematics_env_values`
:   A list of the values and variables that need to be passed to the Schematics service to be used as environment variables during the execution of the Terraform. This might be a secure value, a setting of the Terraform logging or something else. You can choose to specify a string or crete a reference to Secrets Manager. If both are specified, then the Secrets Manager reference is used.

	```json
	{
		"value": "Environment variables and their values",
		"sm_ref": "Specification of an instance of Secrets Manager and a key"
	}
	```
	{: codeblock}

`terraform_version`
:   The Hashicorp Terraform runtime version that is needed to validate and install the version. Setting this value in the manifest overrides what is specified in the source code.

`outputs`
:   Section header for information about Terraform output values.

	```json
	{
		"key": "name of the output value as defined in the Terraform",
		"description": "The description of the key"
	}
	```
	{: codeblock}

   `key`
   :   Specifies the output value.

   `description`
   :   A short summary of the output value.

`install_type`
:   Specifies whether a deployable architecture is full stack or extension. Architectures listed as extensions require prerequisites.


`scripts`
:   A list of scripts contained within the same repository that can be run by a project during a particular stage of a specified action. Each key in the map must match the format `action` and `stage` in the entry. `Stage` must be either `pre` or `post`. `Action` must be `validate`, `deploy`, or `undeploy`.

	```json
	{
		"short_description": "description for the script",
		"type": "type of script. i.e. ansible",
		"path": "the path to the script in the repo. Must begin with scripts/..."
		"stage": "pre or post"
		"action": "The action that executes the script. Options include validate, deploy, or undeploy."
	}
	```
	{: codeblock}
