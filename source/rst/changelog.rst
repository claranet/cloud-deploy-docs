.. _changelog:

.. title:: Changelog

Release Changelog
=================

.. toctree::
    :maxdepth: 2


Cloud Deploy v18.10
-------------------

* WebUI
    - [GHOST-601] - Dynamically list instance types using AWS Pricing API

* Core/API
    - [GHOST-76]  - Hot reload credentials when accounts.yml has changed on disk
    - [GHOST-625] - Expose standard webhooks and allow CI integration (Bitbucket, Github, Gitlab, custom handlers)
    - [GHOST-552] - Add and force authentification on websocket server

* Improvements & Bug fixes
    - [GHOST-686] - Safe deploy with multiple ALB and TargetGroups on multiple ASG: we must not wait for draining on unrelated Targets
    - [GHOST-687] - Safe deploy with multiple ALB and TargetGroups on multiple ASG: don't deregister unrelated instances
    - [GHOST-689] - Module path inclusion check should handle only nested directories
    - [GHOST-481] - Stage1 Bootstrap enhancement and boot deploy notifications

* Misc
    - [GHOST-692] - Update dependencies
    - [GHOST-693] - Update instance types - AWS China EC2 types
    - [GHOST-690] - Use https for Github public submodules

Cloud Deploy v18.08
-------------------

* WebUI
    - [GHOST-161] - Provide search for deployments page
    - [GHOST-191] - Filters improvements
    - [GHOST-672] - Properly display "Log file not found" error in the WebUI

* Core/API
    - [GHOST-507] - Module deployment from AWS S3 (new type of module)
    - [GHOST-406] - Data access layer, to normalize objects retrieved from the backend
    - [GHOST-664] - Major updates of dependencies with breaking changes (Flask, Cerberus, Eve)
    - [GHOST-556] - Move websocket (real time logs) from UI to API core
    - [GHOST-677] - boto sts assume role as an autonomous pip package

* Improvements & Bug fixes
    - [GHOST-678] - Do not allow modules with conflicting paths
    - [GHOST-679] - Fix bug to pass environment variables as parameter on each necessary LXD container execute method
    - [GHOST-681] - Buildimage fails when AWS assume-role is required

* Documentation
    - [GHOST-680] - how to configure features and provisoners

* Misc
    - [GHOST-674] - Update dependencies
    - [GHOST-675] - Update instance types

Cloud Deploy v18.06.1
---------------------

* Improvements & Bug fixes
    - [GHOST-584] - Upgrade job email templates (more compatible mail clients)
    - [GHOST-669] - [UI] - Can't update scripts area after adding a new env var entry

Cloud Deploy v18.06
-------------------

* WebUI
    - [GHOST-661] - LXD endpoint check and UI update to use the API

* Core/API
    - [GHOST-660] - Protect blueprints with Eve authentication
    - [GHOST-584] - Email account information upon creation (using One time secret service for retrieving your password)
    - [GHOST-651] - Use ``/ghost`` working directory for backup instead of ``/tmp``

* Improvements & Bug fixes
    - [GHOST-537] - [Refactor] Image builder lib refactoring and improvements (for both LXD builder and AWS AMI builder)

* Misc
    - [GHOST-666] - Update dependencies
    - [GHOST-667] - Update instance types
    - [GHOST-658] - CI - Bitbucket Pipeline cleanup with ``pylxd 2.2.7``

Cloud Deploy v18.05.1
---------------------

* WebUI
    - [GHOST-495] - [UI] Display instance tags in app resources view, highlight invalid tags regarding the app configuration
    - [GHOST-574] - [UI] Show if running instances for a specific app are not based on the current app AMI
    - [GHOST-529] - [API/UI update for CLI] Live command logs 😎

* Core/API
    - [GHOST-638] - Send emails only for jobs in a specific state (only failed for example)
    - [GHOST-523] - [API update for CLI] Allow to see/download command logs

* Improvements & Bug fixes
    - [GHOST-647] - [UI] Update feature details modal title
    - [GHOST-649] - [UI] Update ``psutils.virtual_memory()`` return tuple (Hotfix, breaking change with psutils 5.4.4)

* Misc
    - [GHOST-648] - [CI] Split UI and Core pipeline/tests


Cloud Deploy v18.05
-------------------

* WebUI
    - [GHOST-573] - Fix job logs with special characters that weren't fully displayed (text encoding)
    - [GHOST-294] - [UI] Add customizable shortcuts actions on home page
    - [GHOST-567] - Display job duration in web UI
    - [GHOST-626] - Display friendly region name in UI
    - [GHOST-627] - Make env & role fields read only during edits
    - [GHOST-634] - Move specific UI ``aws_data`` to ``web_ui/data``
    - [GHOST-644] - Update AWS EC2 instance types

* Core/API
    - [GHOST-633] - Update app updates check function to fix incompatibility with terraform provider
    - [GHOST-639] - Fix root block size issue when using both root and optional block devices, config update in command ``buildimage`` using ``Packer``
    - [GHOST-632] - Expose Cloud Deploy (Ghost) version in API
    - [GHOST-635] - Change error return code when app already exists (HTTP 409)
    - [GHOST-608] - Make app name, env and role fields immutable

* Improvements & Bug fixes
    - [GHOST-600] - Error 500 on POST /apps if no modules
    - [GHOST-493] - Improve ``stage2`` (bootstrap and deploy script) checks to avoid loop until timeout
    - [GHOST-636] - [Core] Revamp git lock algorithm (prevent concurrent access errors)

* Misc
    - [GHOST-643] - Update pip dependencies
    - [GHOST-641] - Update CI and use private Docker registry

Cloud Deploy v18.04
-------------------

* Global
    - [GHOST-563] - Add a new ``description`` field to application, shown as tooltip in UI (app list)
    - [GHOST-597] - Update dependencies (pip)
    - [GHOST-598] - Update instance types
    - [GHOST-599] - Update changelog

* WebUI
    - [GHOST-461] - Disable submit button while loading (ajax call) on command page, prevent from submitting incomplete HTML form.
    - [GHOST-549] - Fix display bug on resource details (wrong label size)
    - [GHOST-557] - Fix remote file inclusion vulnerability on websocket
    - [GHOST-573] - Incomplete job display with some Latin/ISO characters
    - [GHOST-559] - Enable header layout templating for instance distinction: background image, menu color or custom logo

* Core/API
    - [GHOST-613] - Replace deprecated Packer ``ssh_private_ip`` option, requires Packer > ``v1.2.0``
    - [GHOST-577] - Add new AWS region ``eu-west-3`` (Paris) support
    - [GHPST-629] - [API] - Disable ``replace`` CRUD method (``PATCH verb``) in Eve

* Improvements & Bug fixes
    - [GHOST-615] - Fix - Command deploy crashes when ``safe_deployment`` isn't defined
    - [GHOST-622] - Job exception when ``log_notifications`` is not defined

* System update
    - [GHOST-559] - Deployment of specific ```config.yml`` for UI
    - [GHOST-577] - Upgrade to Packer ``v1.2.1``

Cloud Deploy v18.03
-------------------

* Global
    - [GHOST-587] - ``ghost-doc`` CI - Bitbucket Pipeline
    - [GHOST-593] - Update dependencies
    - [GHOST-594] - Update AWS EC2 instance types
    - [GHOST-595] - Update documentation changelog

* WebUI
    - [GHOST-604] - UI exception when LXD endpoint is down, better check on LXD endpoints
    - [GHOST-532] - trim the ``path`` parameters of a module

* Core/API
    - [GHOST-586] - Trigger a ``git prune`` on local mirrors to cleanup bad git objects
    - [GHOST-519] - More options for Packer instances, uses private SSH connection and a custom SecurityGroup
    - [GHOST-564] - Too many open files when deploying, trigger ``git gc`` on local mirrors
    - [GHOST-606] - Fix API exception on /lxd/images path
    - [GHOST-607] - Fix local permissions of previous deployment workspace
    - [GHOST-553] - [api] Refactor 422 (wrong user input) error codes and give more explicit messages

* Improvements & Bug fixes
    - [GHOST-534] - No job log sent to S3 when notification email fails
    - [GHOST-540] - ``buildimage`` fails if an environment variable has no value
    - [GHOST-542] - Fix an error at deploy related to blue/green options

* System update
    - [GHOST-541] - [ghost update] Remove ghost version from role, version need to be specified
    - [GHOST-558] - [ghost update] Build documentation when deploying and remove artefacts from git

Cloud Deploy v18.02
-------------------

* Global
    - [GHOST-544, GHOST-545, GHOST-548] - Global repository revamp
        - CORE/API code ready to be published in public
        - Web UI still under proprietary license, available only for Claranet customers
        - Submodules updates to use public git repositories

* Core/API
    - [GHOST-543] - Disable SSH known_hosts check in Fabric

* Improvements & Bug fixes
    - [Hotfix GHOST-73] - Fix ``execute_module_script_on_ghost`` function call on redeploy command
    - [GHOST-518] - Allow to disable tar warning if file timestamps are in the future during extraction

* System update
    - [GHOST-578] - [Role update] Update setuptools version in virtualenv, needed for old Debian instances

Ghost 17.12.1
-------------

* WebUI
    - [GHOST-63] Feature - Ansible Role dynamic parameters and SaltStack formula list from Inventory JSON Schema
        UI form is based on the schema declared for each Ansible role and displays an appropriate input for each available role parameter (Ansible variable).

* Core/API
    - [GHOST-63] Feature - Ansible Role dynamic parameters
        All Ansible Role parameters can now be a generic object passed to the API (Serialized by the Web UI) and used when baking images via the ``buildimage`` command.

Ghost 17.11.1
-------------

* Core/API
    - [GHOST-520] - Update AWS EC2 Instance type list with new M5, H1 and X1E types
    - [GHOST-474] - Update packer from 0.12.2 to 1.1.2

* Improvements & Bug fixes
    - [GHOST-220] - Requirements dependencies update (pip packages)

Ghost 17.11
-----------

* Global
    - [GHOST-73] - *New optional feature*: ``buildpack`` in a secure isolated environment (a container).
        An LXC image is now built at ``buildimage`` and when deploying, the ``buildpack`` step is launched in an isolated LXC container (based on the generated image).
        Please check :ref:`LXC/LXD build section <container>` for more information

.. warning:: Using the container feature with LXC/LXD requires to have an up-to-date Ghost instance OS (Debian 9+ or Ubuntu 16+).

Ghost 17.10
-----------

* CLI
    - [GHOST-492] - [Casper] Overall CLI upgrade and refactoring (Please check :ref:`CLI section <cli>` for more information)

* Core/API
    - [GHOST-514] - Ansible provisioner: debug level option (log verbosity when using ``buildimage`` command)
    - [GHOST-520] - Update AWS EC2 Instance type list with new C5, P3, F1 and X1E

* Improvements & Bug fixes
    - [GHOST-483] - [API] Unable to enable BlueGreen on some old application
    - [GHOST-508] - Can't use default xvda as default root device with AWS Debian Strech AMI

* System update
    - [GHOST-485] - [Upgrade Ansible Role] Restart supervisor service instead of reload
    - [GHOST-514] - Ansible provisioner: debug level parameter available when deploying Ghost upgrade

Ghost 17.09.1
-------------

* WebUI
    - [GHOST-500] - [UI] Parse deployments timestamp as Date (``RFC1123_DATE_FORMAT`` format)
    - [GHOST-482] - [UI] Allow to copy code in modal windows
    - [GHOST-473] - [UI] Optional Volume Device Name App field's documentation does not match API

* Core/API
    - [GHOST-477] - Add link to job in email notification
    - [GHOST-496] - Ensure git mirror locks are released in case of failure

* Improvements & Bug fixes
    - [GHOST-481] - Stage1 Bootstrap enhancement
    - [GHOST-475] - Cleanup Stage2 and remove Salt dependency
    - [GHOST-494] - Remove Ansible provisioner Bootstrap (no longer needed with Ansible remote execution)

Ghost 17.09
-----------
* WebUI
    - [GHOST-472] - [UI] Fix - Delete Optional Volume button doesn't work on first item

* Core/API
    - [GHOST-459] - [BlueGreen] - Blue/Green properly handle managed LoadBalancers
    - [GHOST-465] - [BlueGreen] - Add pre and post swap BlueGreen hooks
    - [GHOST-453] - Add option to create and attach additional EBS volumes during ``buildimage`` with packer
    - [GHOST-445] - Use our own git lock system to avoid concurrent access on local git mirrors

* Improvements & Bug fixes
    - [GHOST-466] - ``/etc/hosts`` modifications by stage2 are rewritten on reboot on some Debian Jessie instances
    - [GHOST-470] - [CI] - Improve BitBucket pipeline performance
    - [GHOST-471] - [BlueGreen] - LoadBalancer Health check is not restored in case of error or roll back during swap
    - [GHOST-478] - [API] - Fixing IAM ``instance_profile`` name length range

* Documentation
    - [GHOST-459] - [BlueGreen] - New option introduced: creates the temporary LoadBalancer when triggering ``preparebluegreen``
    - [GHOST-465] - [BlueGreen] - Current active color is now an environment available variable
    - [GHOST-465] - [BlueGreen] - ``swapbluegreen`` detailed diagram flow
    - [GHOST-464] - Some documentation improvements

Ghost 17.08.1
-------------
* Core/API
    - [GHOST-374] - Ansible provisioner generic bootstrap script (for Packer)
    - [GHOST-374] - Ansible provisioner full implementation

* Improvements & Bug fixes
    - [GHOST-426] - Provisioner unit test with mocks

* Documentation
    - [GHOST-374] - Ansible usage when baking Images with ``buildimage`` command
    - [GHOST-464] - Global documentation update

Ghost 17.08
-----------

* WebUI
    - [GHOST-452] - [UI] Fix - Logout mechanism is buggy
    - [GHOST-460] - [UI] "Click to expand" text on code blocks stay visible for new modules
    - [GHOST-463] - [UI] Special characters in user's input script crash the application view

* Core/API
    - [GHOST-456] - Cannot go back to Root Block Device Name default value once it has been set
    - [GHOST-312] - Zabbix Hostname is now set with IPv4 suffix (using dots instead of dashes)
    - [GHOST-458] - [API] Filter available commands by application context

* Improvements & Bug fixes
    - [GHOST-454] - Proposed commands: ``updateautoscale`` is proposed even if app has no auto scale group
    - [GHOST-220] - Requirements dependencies update (pip packages)
    - Available AWS EC2 instance types updated (with g3 and p2 types)

Ghost 17.07
-----------

* WebUI
    - [GHOST-431] - [UI] Answering "no" to the delete action make the user redirect to object list page
    - [GHOST-419] - [UI] Messages when saving an app - propose which commands to launch based on modified fields
    - [GHOST-427] - [UI] Refactor code macro, templates, models, and Javascript imports
    - [GHOST-437] - [UI] Switch on Material Kit theme and improve UI/UX

* Core/API
    - [GHOST-443] - [API] Verify script b64 validity
    - [GHOST-438] - [API] Forbid ``/ghost`` as module folder
    - [GHOST-414] - Create a Ghost update script
    - [GHOST-262] - Avoid deleting an used LaunchConfiguration (and also rewrite all purge mechanism)

* Improvements & Bug fixes
    - [GHOST-440] - [API] Updating an app with API call fails when ``environment_infos`` field is missing
    - [GHOST-450] - [UI] Wrong ALB are displayed on Resources Details View

* Documentation
    - [GHOST-449] - [DOC] Update deploy workflow with more details

Ghost 17.06.1
-------------

* WebUI
    - [GHOST-435] - [UI] Use ``format`` in all forms functions helper to prevent formatting errors

* Core/API
    - [GHOST-424] - The comma char is now allowed in feature value field

* Improvements & Bug fixes
    - [GHOST-442] - [UI] App Command - retrieve revisions function (was broken in previous version)
    - [GHOST-433] - Upgrading from an older Ghost version breaks AutoScaling tag Name

* Documentation
    - [GHOST-356] - ``updateautoscaling`` no longer updates ASG's desired

Ghost 17.06
-----------

* WebUI
    - [GHOST-417] - [UI] Module deployment state (in ``app_view``, ``app_command``, ``app_list``)
    - [GHOST-394] - [UI] 404 Page, don't show ``back button`` after an object deletion
    - [GHOST-416] - [UI] Fix - Draggabble feature is not editable on Firefox v54

* Core/API
    - [GHOST-422] - [Mail Notifications] Notifications do not show the correct job end date and time
    - [GHOST-313] - [bluegreen] Handle ALB in BlueGreen commands
    - [GHOST-407] - [stage2] Use ``--only-show-errors`` for ``aws s3 cp`` call - less verbose log
    - [GHOST-409] - [command/deploy] Reduce Deploy package size by excluding git metadata (optional)
    - [GHOST-220] - Update python dependencies

* Improvements & Bug fixes
    - [GHOST-410][GHOST-412] - [Blue/Green] Manage all listeners on ELB copy
    - Hotfix [GHOST-375] - Import ``ghost_abbrev_field`` macro
    - [GHOST-430] - Include Nginx & Supervisor config in backup/restore scripts
    - [GHOST-434] - [UI] An AMI without name make application form crash

* Documentation
    - [GHOST-391] - BlueGreen documentation update
    - [GHOST-183] - Upgrade Sphinx doc lib
    - [GHOST-337] - Some more script example in ``bestpractices`` page

Ghost 17.05.1
-------------

    - [GHOST-375] - [UI][Core][Commands] New ``executescript`` command

.. seealso:: :ref:`cmd_executescript` command documentation for more details.

Ghost 17.05
-----------

* WebUI
    - [GHOST-345] - [UI] Revamp and unify ``app_list`` views + improvements and fixes
    - [GHOST-388] - Better large logs loading behavior (less browser freezes, support very large logs)
    - [GHOST-389] - [UI] Defer CodeMirror initialization to improve page rendering on ``app_edit`` view
    - [GHOST-399] - [UI] Service ``get_ghost_app_ec2_instances`` must also filter on Ghost color tag if blue green is enabled

* Core/API
    - [GHOST-387] - Choose a provisioner per feature
    - [GHOST-390] - Unify Ghost job status color on Slack and eMail notifications
    - [GHOST-396] - Make EC2 public IP assignment optional

* Improvements & Bug fixes
    - [GHOST-313] - Writing tests for blue/green commands and most of elb/alb functions
    - [GHOST-345] - [UI] Fix pagination limit and env_list function
    - [GHOST-385] - Use python gzip to compress mail attachment
    - [GHOST-386] - Allow overriding endpoints configs using environment variables
    - [GHOST-392] - HotFix BlueGreen AMI info copy
    - [GHOST-397] - Error on salt repository clone raises an import error
    - [GHOST-400] - Remove default mutable arguments
    - [GHOST-402] - Fix apache/PHP feature preset
    - [GHOST-405] - [UI] Avoid AWS API Throttling Rate exceeded errors

* Documentation
    - [GHOST-403] - [``recreateinstance``] Add LoadBalancer workflow information

Ghost 17.04
-----------

* WebUI
    - When ``Use a custom identity`` is unchecked, reset all identity params to default values [GHOST-366]
    - Add logout link button [GHOST-381]
    - Job status color background [GHOST-384]

* Core/API
    - RQ Worker job timeout value should be configurable [GHOST-379]
    - Setting min value for root block size (20GB) [GHOST-373]
    - Option to enable AutoScaling metrics (option applied when using ``updateautoscaling`` command) [GHOST-382]
    - Document and revamp ``config.yml.sample`` file [GHOST-380]
    - Store Job logs into S3 bucket [GHOST-297]

* Improvements & Bug fixes
    - Refactor ``buildimage`` command with a generic builder interface [GHOST-376]
    - Uses ``Claranet Cloud Deploy`` for Slack bot name [GHOST-372]
    - Fix Safe Deploy option in ``redeploy`` command [GHOST-377]
    - UI HTML structure improvements + CSS/JS fixes [GHOST-348]

* Documentation
    - OpenAPI/Swagger attributes adjustment for ReDoc and using ReDoc interface [GHOST-378]

Ghost 17.03
-----------

* WebUI
    - Product renamed to ``Claranet Cloud Deploy`` in WebUI [GHOST-372]
    - Fix UI filter per env when it contains dashes [GHOST-352]

* Core/API
    - Update python dependencies [GHOST-357][GHOST-220]
    - New command ``recreateinstances`` that allow to safely renew instances with or without an Auto Scaling Group (Rolling update strategy). Please check :ref:`cmd_recreateinstances` documentation for more information. [GHOST-293]
    - New option to purge old Ghost packages in S3 Bucket [GHOST-38]
    - Refactoring of Feature provisioner class (SaltStack), ready to handle Ansible as new provisioner [GHOST-353]
    - Refactoring on ``find_ec2_instances`` function [GHOST-368]
    - Generic Ghost restore script [GHOST-362]

* Improvements & Bug fixes
    - Introduce py.test unit testing [GHOST-342]
    - Keep ELB attributes when making the ELB copy [GHOST-343]
    - Default ``subnet_id`` value is not set for ``createinstance`` command [GHOST-358]
    - Handle missing module errors in ``auth.py`` script [GHOST-370]
    - Instance has to be in running state in order to be tagged with the ``createinstance`` command [GHOST-229]
    - ``gzip -k`` is not available on Debian 7 Wheezy [GHOST-369]

* Documentation
    - Using ``Claranet Cloud Deploy`` name [GHOST-372]
    - Detailed workflow diagrams for ``Safe deploy option`` [GHOST-142]
    - ``buildimage`` workflow updated, multiple provisioner supported [GHOST-353]
    - Global changelog, home and quick-start page fixes [GHOST-183][GHOST-367]
    - New documentation page about general guidance for scripting in Ghost [GHOST-337]

Ghost 17.02
-----------

* WebUI
    - Adding new ``env`` field values is possible from the web UI [GHOST-360]

* Core/API
    - Update python dependencies [GHOST-357]
    - The ``env`` attribute is now generic [GHOST-360]
    - Slack notifications available [GHOST-7]
    - HTML Mail template for job notifications (replaces the raw text format) [GHOST-345]
    - AutoScale ``current/DesiredCapacity`` value should not be handle in Ghost [GHOST-356]

* Improvements & Bug fixes
    - Fix: ``preparebluegreen`` command was broken (``as_conn`` variable missing) [GHOST-361]
    - Fix: remove the first character (/) of legacy MANIFEST path when using blue-green deployment [GHOST-364]
    - Refactor LaunchConfiguration creation and ASG update functions [GHOST-355]
    - Strip git repo url to avoid errors [GHOST-346]

Ghost 17.01
-----------

* WebUI
    - Ghost instance health status (footer link) [GHOST-204]
    - Orange warning color when choosing a big instance type [GHOST-338]
    - Adding z-index for footer, updating left bar height dynamically [GHOST-325]
    - Fix infinite scrolling to work with zoomed in or out view [GHOST-302]
    - Fix getting last deployed revision in Run More Like This context [GHOST-332]
    - Keep UI app_list view mode (tabbed) in a cookie [GHOST-321]
    - List git available branches and tags on ``deploy`` command [GHOST-296]

* Core/API
    - Do not install curl before bootstrapping SaltStack (requires Packer v0.12.1+) [GHOST-334]
    - Option “Destroy temporary CLB” for ``purgebluegreen`` command [GHOST-303]
    - Verify deployed module name too when using ``preparebluegreen`` [GHOST-287]
    - A dedicated queue and worker is now available per app color when Blue-green is enabled [GHOST-288]

* Improvements & Bug fixes
    - Ensure Ghost tags are properly set (on AutoScale and standalone instances) [GHOST-336]
    - Fetch SaltStack formulas git submodule only if needed [GHOST-351]

* Documentation
    - Upgrade to eve-swagger 0.0.6 [GHOST-349]
    - New documentation page - Ghost best practices [GHOST-337]

Ghost 16.12
-----------

* WebUI
    - Handle ALB/TargetGroups in UI (app infos) [GHOST-310]

* Core/API
    - Handle Application Load Balancer in SafeDeployment [GHOST-310]
    - Correct ASG boto2 errors when ALB is used by upgrading to boto3 [GHOST-309]
    - Keep a local mirror of morea-salt-formulas & zabbix Git repos [GHOST-271]
    - Allow creating Launch Configurations with Detailed EC2 Instance Monitoring enabled, on a per app basis [GHOST-162]
    - Move to eve-swagger for API documentation [GHOST-329]

* Improvements & Bug fixes
    - Hotfix "Run more like this" (caused by GHOST-291) [GHOST-330]
    - Docker-compose: add nginx container for better local tests [GHOST-331]
    - Upgrade to boto v2.45.0 (handle new AWS regions: eu-west-2, ca-central-1, us-east-2, ap-south-1) [GHOST-339]
    - Colorized error messages in stage2 [GHOST-340]
    - Create empty MANIFEST if nonexistent upon successful buildimage to allow instance bootstrapping [GHOST-341]
    - Ensure app/env/role Ghost tags are properly set when using ``updateautoscaling``, ``createinstance`` and ``preparebluegreen`` commands [GHOST-336]

Ghost 16.10
-----------

* WebUI
    - Replace Morea by Claranet in the webUI [GHOST-308]
    - Handle ``createinstance`` job in ``Run more like this`` action [GHOST-291]
    - Use tabs per env for app list [GHOST-307]

* Core/API
    - Add ssh config to backup [GHOST-314]

* Improvements & Bug fixes
    - Init provider JS param when cross account activated [GHOST-295]
    - Using / instead of /apps to check auth  which could hurt performance [GHOST-322]
    - Move get_envs call to specific template that need it [GHOST-322]
    - Command ``swapbluegreen`` should stop when the offline ELB is not correctly configured [GHOST-292]
    - Add suspend and resume AutoScaling process in ``preparebluegreen`` command [GHOST-327]
    - Docker-compose update to version 2 [GHOST-320]
    - Use mongo and Redis endpoints config in commands [GHOST-318]
    - Adding jetbrains clauses to gitignore [GHOST-315]

Ghost 16.09.1
-------------

* Improvements & Bug fixes
    - Update boto3, botocore and awscli dependencies [GHOST-311]
    - Fix ``preparebluegreen`` command options [GHOST-229]
    - Hotfix - use custom app tags only if set [GHOST-243]
    - Fix ASG listing when ALB are associated by using boto3 [GHOST-309]

Ghost 16.09
-----------

* WebUI
    - CodeMirror scripts upgrade - better script area in UI [GHOST-215]
    - Show Optional volumes in ``app_view`` [GHOST-306]
    - Format Packer output with HTML [GHOST-298]

* Core/API
    - Allow custom EC2 Tags per application, auto applying Ghost specific Tags [GHOST-243/GHOST-244]
    - Handle per application custom environment variables. Thoses variables will be available in many scripts from the ``deploy`` and ``build`` workflow. (more details here: :ref:`scripts_vars`) [GHOST-216]
    - Rollback application manifest if a ``deploy`` or ``redeploy`` command fails [GHOST-286]
    - Feature preset import, permits to bulk import some features in an application based on ready-to-use preset [GHOST-133]
    - Add seconds when generating LaunchConfig name to avoid naming collisions [GHOST-301]
    - Docker compose file and Redis/Mongo endpoints configurable [GHOST-153]

* Improvements & Bug fixes
    - An AutoScale Group is now mandatory to use Safe Deploy [GHOST-280]
    - Stage2 script now follows symlinks when updating Zabbix config [GHOST-285]
    - Version field in feature can be empty/null [GHOST-270]
    - Available AWS EC2 instance types updated
    - Python modules upgraded (boto*)
    - Hotfix GHOST-229: don't show ``blue`` bubble when BG is not enabled

Ghost 16.07.1
-------------

* Improvements & Bug fixes
    - Hotfix [GHOST-229]: fix redeploy command broken by refactoring
    - Hotfix [GHOST-229]: boto3 addition upgrades botocore which breaks awscli 1.4 (from wheezy) so also update awscli

Ghost 16.07
-----------

* WebUI
    - Add ``Documentation`` link in footer [GHOST-183]
    - WTForm SelectField override to handle no available selected data [GHOST-278]
    - Show S3 link to module package in Deployment view [GHOST-277]
    - Also display AMIs from specific third party AWS accounts [GHOST-276]
    - [UI] Drag'n'drop Features order [GHOST-274]

* Core/API
    - Blue/Green deployment strategy [GHOST-229] (more info here: :ref:`bluegreen`)
    - Add ami-base role for base AMI building [GHOST-275]
    - Role field now generic (a specific role can be created) [GHOST-241]

* Improvements & Bug fixes
    - Clean Error for empty boostrap during stage2 execution [GHOST-249]
    - Refactor ``destroyallinstances`` command [GHOST-273]
    - Hotfix [GHOST-102] show Ghost tag instances bug

Ghost 16.06
-----------

* WebUI
    - [UI] Quick access boutons on "Completed view" [GHOST-252]
    - JS Fix for Cross Account credential check [GHOST-267]

* Core/API
    - Add generated hostname to /etc/hosts for private IP resolution [GHOST-251]
    - Add private IP option and Subnet option in ``createinstance`` command [GHOST-248]
    - AMI retention purge is now configurable [GHOST-259]
    - Handle fabric errors, Job will be marked as failed if one ``predeloy`` or ``postdeploy`` script fails [GHOST-265]
    - ghost-doc repo as Submodule [GHOST-183]
    - Add the 'After all deploy' script available, triggered on Ghost after the deployment on every instances [GHOST-255]
    - Pre and Post Buildimage hooks, custom scripts to tweak AMI if needed [GHOST-253]
    - Features with multiple pillar parameter values, allow us to be more flexible on SaltStack formulas [GHOST-270]
    - Handle UTF-8 characters in base64 encoded scripts (pre-bootstrap, post-bootstrap, buildpack, pre-deploy, post-deploy, after-all-deploy, pre-buildimage, post-buildimage) [GHOST-264]

* Improvements & Bug fixes
    - Fix Safe Deployment with cross account and spaces issue [GHOST-142]
    - getconf HOST_NAME_MAX to truncate hostname [GHOST-263]
    - Allow installation of arbitrary gems [GHOST-258]
    - Fix to handle buttons when creating/cloning an app [GHOST-252]
    - Update subnets in ``updateautoscale`` command [GHOST-260]
    - use boto.s3.connection.OrdinaryCallingFormat() calling format to support bucket with dots in their name [GHOST-256]

Ghost 16.05.2
-------------

* Global
    - Gestion du multi compte AWS (utilisation du AWS STS Assume Role pour gérer les ressources sur le compte distant) [GHOST-208]

* WebUI
    - Le header et son menu sont maintenant responsives (compatibilité Mobile) [GHOST-254]

* Core/API
    - Possibilité d'utiliser multiples clé SSH dans Ghost pour les déploiements (par région, par compte, par env, par app, etc.) [GHOST-225]

Ghost 16.05.1
-------------

* Core/API
    - Nouveaux environnements disponibles: int, uat, oat [GHOST-247]
    - Ajout de l'IP privé des instances démarrées par Ghost dans le Hotname (et par extension dans le PROMPT PS1) [GHOST-250]
    - Spécification d'un AWS IAM Instance Profile spécifique au lancement de Packer. Permet d'avoir des policy AWS qui pourraient être nécessaire au ``buildimage`` [GHOST-245]

* Améliorations & Correctifs de bogues
    - Ajout de l'option ``ssh_pty`` à l'appel Packer (nécessaire sur RedHat/CentOS) [GHOST-246]


Ghost 16.05
-----------

* WebUI
    - Ajout de descriptions sur l'ensemble des champs lors de l'édition d'application [GHOST-236]
    - Better Job Log view (Possibilité de collapse/expand les commandes, coloration, ajout du temps d'exécution de chaque commande) [GHOST-199]
    - Améliorations du footer (meilleure gestion de la version Ghost à afficher) [GHOST-218]
    - Boutton de refresh pour les listes de Subnet et de SecurityGroups [GHOST-167]
    - Possibilité de déployer plusieurs ou tous les modules avec la commande ``deploy`` [GHOST-240]

* Core/API
    - La commande ``updatelifecyclehooks`` doit aussi mettre à jour l'AutoScale (LaunchConfig userdata) [GHOST-168]
    - La commande ``buildimage`` ne clone que la branche SALT nécessaire au provisionning [GHOST-206]
    - Les scripts ``stage1`` et ``stage2`` utilise le binaire AWS (cli) depuis le $PATH [GHOST-235]
    - Nouveau role disponible: 'webcache' [GHOST-222]
    - Possibilité d'utiliser la nouvelle option ``Safe Deployment`` avec la commande deploy [GHOST-142]
      Plus d'informations sur la documentation: https://demo.ghost.morea.fr/doc/rst/commands.html#run-deploy

* Améliorations & Correctifs de bogues
    - Packer provisionne curl uniquement si il faut installer SALT (Skip Salt Bootstrap option) [GHOST-234]
    - Possibilité d'utiliser `ec2-user` à la place d'`admin` [GHOST-231]
    - Meilleure gestion des erreurs d'API AWS dans la WebUI [GHOST-233]
    - Ajout des nouveaux types de Volume EBS AWS [GHOST-238]
    - Meilleure gestion des erreurs sur le nettoyage des scripts au stage2 (pre-deploy, post-deploy, buildpack) [GHOST-232]
    - Suppression des fichiers temporaires sur Ghost (Manifest tempon) [GHOST-230]
    - Plus besoin de chown dans le script stage2 les dossiers des modules avant déploiements (les modules ont pour UID et GID les valeurs spécifiées dans l'app) [GHOST-237]

Ghost 16.04
-----------

* WebUI
    - Ajout des types d'instances EC2 sur la région Chine (cn-north-1) [GHOST-219]
    - Désactivation de l'auto-scroll sur la vue log d'un job quand l'utilisateur utilise sa molette [GHOST-223]
    - Refonte du header et ajout d'un footer avec la version courante de Ghost [GHOST-218]
    - Ajout des descriptions des commandes [GHOST-217]

* Core/API
    - Le nombre de LaunchConfig à conserver sur l'AutoScaling pour pouvoir Rollback est maintenant configurable [GHOST-195]
    - Configuration automatique du Hostname des instances démarrées par l'AutoScaling [GHOST-226]
    - Mise à jour des dépendances Python (requirements.txt) [GHOST-220]
    - A la suppression d'un module, nettoyage des dossiers locaux liés au module supprimé [GHOST-177]
    - Possibilité de choisir si Packer doit installer Salt avant de provisionner l'AMI [GHOST-171]

* Améliorations & Correctifs de bogues
    - Correctifs sur le script de sauvegarde Ghost, permet l'automatisation de sa mise en place [GHOST-224]
    - Déplacement de la valeur PAGINATION_DEFAULT de settings.py vers config.yml [GHOST-175]

Ghost 16.03
-----------

* WebUI
    - Possibilité de ré-ordonner les modules d'une application Ghost via drag'n drop sur le menu de gauche [GHOST-113]
    - Commande "deploy" par défaut [GHOST-205]
    - Nouveau style pour les boutons d'actions sur les listes [GHOST-207]
    - Bouton pour rafraîchir les Select (peuplés depuis AWS) sur l'édition d'application [GHOST-167]
    - Coloration syntaxique shell/bash pour les Textarea, avec numérotation de ligne et police à taille fixe  (pre-deploy, post-deploy, buildpack) [GHOST-215]

* Core/API
    - Création du dossier de destination lors du déploiement d'un module si celui-ci n'existe pas (script stage2) [GHOST-212]
    - Lors d'un Deploy/Re-Deploy, le manifest est re-ordonné suivant l'ordre des modules définis dans l'application Ghost [GHOST-113]
    - Nouvelles variables d'environnement disponibles pour les scripts de pre-deploy & post-deploy [GHOST-210]. Pour rappel, voici la liste des variables disponibles :
         * GHOST_APP
         * GHOST_ENV
         * GHOST_ROLE
         * GHOST_MODULE_NAME
         * GHOST_MODULE_PATH
         * GHOST_MODULE_USER
         * GHOST_MODULE_REPO
         * GHOST_MODULE_REV
         * GHOST_MODULE_COMMIT
         * GHOST_MODULE_COMMIT_MESSAGE
    - Nouvelle commande "Update auto scaling group" disponible [GHOST-48]

* Améliorations & Correctifs de bogues
    - Amélioration du nettoyage des anciennes révisions de modules sur les instances (libération d'espace disque) [GHOST-211]
    - Utilisation de noms explicites pour les fichiers de logs Packer [GHOST-214]
    - Refactoring de la commande Create Instance [GHOST-169]

Ghost 16.02
-----------

* WebUI
    - Vue sur les Ressources AWS d'une application (AS, ELB, Instances EC2) [GHOST-102]
    - Thème Material Design (guidelines Google) [GHOST-143]
    - Auto-complétion sur les listes [GHOST-170]
    - Button pour mettre la console de log (vue Job) en mode théâtre [GHOST-188]
    - Protection du double clic sur les boutons de validation (évite de lancer 2 jobs) [GHOST-180]
    - Récupération des KeyPairs & Instances Profiles depuis API AWS [GHOST-178]

* Core/API
    - 3 Stratégies de Worker possibles pour une instance Ghost : 1 par app, 1 par env, 1 pour l'instance [GHOST-193]
    - Possibilité de définir les UID & GID des fichiers déployés par un module [GHOST-187]
    - Renommage de la commande "Rollback" en "Redeploy" [GHOST-173]
    - Renommage de la commande "Destroy instance" en "Destroy all instances" [GHOST-186]
    - Stratégies de déploiements : Séquentiel ou parallèle sur les instances (config + option de deploy) [GHOST-82]
    - Suppression des scripts de Predeploy & Postdeploy après exécution [GHOST-189]
    - Suppression du script de Buildpack après exécution [GHOST-190]
    - Déploiement cross-region AWS [GHOST-158]
    - Dépôt SALT configurable [GHOST-157]

* Améliorations & Correctifs de bogues
    - Optimisations sur la récupération des derniers déploiements réussis pour chaque module d'une application [GHOST-172]
    - Refactoring de code [GHOST-163/164/181]
    - Commandes découvertes à la volée [GHOST-30]
    - Attente de la disponibilité des tags sur les instances EC2 avant de continuer les déploiements [GHOST-185]


Ghost 16.01
-----------

* WebUI [GHOST-150, GHOST-155, GHOST-152, GHOST-160, GHOST-138, GHOST-139, GHOST-128, GHOST-55, GHOST-174]
    - Correctif sur la fonction Cloner une Application : rafraichissement des selects
    - Changement des couleurs de fonds sur les listes (retrait du rouge et du vert trop vif remonté par les utilisateurs)
    - Vue liste d'application : recherche et filtres
    - Vue liste des jobs : recherche et filtres
    - La vue Job (détail) se rafraichit automatiquement lors d'un changement d'état
    - Une popover de warning sur le champs Module Path lors de l'édition d'une application si le champ contient une mauvaise valeur : /, /tmp, /etc, /var
    - Défilement infini sur les pages de listes (récupération des données en asynchrones)
    - Logo Ghost & Favicon
    - Fix et correctifs CSS

* Core/API
    - Possibilité d'avoir un dépôt Git spécifique pour les formulas SALT d'une instance Ghost [GHOST-156]
    - Nouvelle commande updatelifecyclehooks : permet d'avoir des scripts de pre_bootstrap et post_bootstrap [GHOST-159]
    - MAX_DEPLOY_HISTORY devient configurable (nombre de révisions de déploiement à conserver) [GHOST-147]
    - Autorisation du caractère "+" dans le champ version des Features [GHOST-145]
    - La variable TMPDIR est définie pour Packer : permet d'avoir les fichiers de logs et temporaires de Packer dans /var/log/ghost/packer [GHOST-166]
    - Nouvelle de stratégie de git clone/pull/mirror sur l'instance Ghost : permet des déploiements beaucoup plus rapides [GHOST-104]

* Script
    - Ghost Backup : possibilité de passer en argument la région S3 de backup (ou spécifiée dans la config de Ghost) [GHOST-146]

* Correctifs de bogues
    - Meilleure prise en compte du code de retour du script pre-deploy [GHOST-151]
    - Meilleur affichage des modules dans les mails de notifications [GHOST-148]
    - Correctif sur le status Auto-scaling (ne doit pas rester en Suspended quand un déploiement échoue) [GHOST-136]

Ghost 15.12
-----------

* Nouvelle interface graphique du client Web [GHOST-44, GHOST-45, GHOST-79, GHOST-93, GHOST-94, GHOST-109, GHOST-115, GHOST-119, GHOST-132, GHOST-134, GHOST-135, GHOST-137]
    - Couleurs pour identifier les environnements _>>> À noter, nous avons déjà eu plusieurs retours négatifs concernant le code couleur utilisé pour distinguer les environnements. Nous allons rectifier le tir dans la version 15.12
    - Picto sur les boutons d’actions (identification plus rapide)
    - Menu flottant sur les vues d’application
    - Header flottant pour mieux voir quel objet est en cours de traitement
    - Plusieurs champs texte remplacés par des Selects pour une saisie plus rapide
    - Revue des valeurs par défaut des champs
    - Amélioration sur la vue « console » (log d’un job)
    - Ajout de RegExp sur le modèle, permet d’éviter des erreurs de caractères non supportés
    - Lien d’accès au dernier déploiement réussi dans la vue Application, tableau de module

* Déploiement parallèle [GHOST-89, GHOST-121]
    - Chaque application possède sa file d’attente de Job
    - Chaque application possède son Worker pour dépiler sa file

* Nettoyage de vieux reliquats [GHOST-36]

* Variable de contexte pour les scripts de Buildpack, Pre-Deploy, Post-Deploy [GHOST-61]

* Possibilité d’annuler un Job qui est en attente (ne peut pas être annulé si déjà démarré) [GHOST-87]

* Meilleure gestion des états d’instances lié aux Auto-Scaling Groups [GHOST-110, GHOST-117]

* Possibilité de choisir le type d’instance EC2 lors du buildimage (peut être différent du type d’instance par défaut de l’application) [GHOST-130]

* Bug fixes [GHOST-108, GHOST-127, GHOST-129, GHOST-131, GHOST-140]

