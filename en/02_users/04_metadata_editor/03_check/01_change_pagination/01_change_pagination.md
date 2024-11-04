# Subsequent changes to pagination

If you wish, you can modify previously created pagination sequences. Goobi allows you to move or delete individual pages or several pages at the same time. To do this, you first need to select the required pages in the `Page selection` box. Once you have highlighted at least one page in this way, you will be able to choose from the following functions:

| Icon                                                                    | Description                 |
| ----------------------------------------------------------------------- | --------------------------- |
| ![screen1.png](<screen1.png>)           | Move the selected page up   |
| ![screen2.png](<screen2.png>)           | Move the selected page down |
| ![screen3.png](<screen3.png>) | Delete the selected page    |

Regardless of whether or not you select a page, you can also use the following function:

| Icon                                                   | Description            |
| ------------------------------------------------------ | ---------------------- |
| ![screen4.png](screen4.png) | Generate new filenames |

If one or more pages are moved up, each page will displace its predecessor in the pagination sequence and will take over all the settings and page allocations of the predecessor. If a page is moved down, its original place it taken by the next page in the pagination sequence.

If the changes affect the image currently being displayed, the image number in the page display is updated automatically. There is no change in the displayed image.

As well as moving files, you can also delete selected files. This action deletes the selected page completely from the metadata file. It affects both filename allocation and allocation to structure elements or allocated metadata.

The file is also deleted from all the process folders. You can search for files that you wish to delete from all the process folders using the selected filename. Goobi will search the available folders for files that match the filename (but not necessarily the file extension). The file will be deleted in all the subfolders of the `ocr` and `images` directories. If the currently displayed image has been deleted, Goobi will display the first image. If not, the image number will be updated.

Goobi also allows you to generate new filenames so that systems that are not based on the sequence of filenames in the METS file can continue to display the images in the correct sequence. All the files are numbered using an eight-digit system based on the sequence in the METS file. The files will be renamed in all the process folders.