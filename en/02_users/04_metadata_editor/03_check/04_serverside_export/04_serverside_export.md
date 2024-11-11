# Server-based exports

A subfolder entitled `fileupload` is automatically generated on the Goobi server in the configured folder named `tempfolder`. This subfolder is used to exchange files between processes on the server.

![Server-based file export](screen_en.png)

In this area of the METS Editor, you can select one or more pages for export to the exchange folder on the server. A subfolder with the current process title is created in the exchange folder. Goobi will search for the selected pages in all the image directories (derivatives) for the current process and export them to the process subfolder in the exchange folder.

You can also choose to delete all the selected pages from the current process when you export them. This deletion will also be applied to the filename allocation, all allocations to structure elements and all the allocated metadata. The file will also be deleted from all the process folders.

If the currently displayed image has been deleted, Goobi will display the first image for that process. If not, the image number will simply be updated.