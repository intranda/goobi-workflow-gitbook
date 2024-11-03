# Automatic script-run steps

As well as the manual scripts described in the last section, Goobi can also be configured to execute individual workflow steps automatically if they have been configured to call up scripts. 

To do this, as for the manual scripts, the administrator will assign a series of different `shell commands` and stipulate that they should be performed automatically one after the other in the specified sequence. Automatic script-run steps are not generally included in a user’s task list. If an error occurs during the execution of the configured server-based script calls with the result that the script cannot actually be executed, the automatic workflow step will keep the same status and will be displayed automatically in the assigned user’s task list. Automatic script-run steps are therefore only visible in the user’s task list if errors occur during execution. 

To identify the error, the user can employ the same method as that described above for manual script-run steps, i.e. by starting the scripts in question manually and thus identifying the source of the error. In cases where the automatic scripts make use of the function allowing users to send information or error messages concerning a specific process, the error messages are also listed in the `Process log` within that task without having to run the script again to identify the error.

Automatic script-run steps that successfully execute the configured scripts automatically close the current workflow step and activate the next step in the workflow.