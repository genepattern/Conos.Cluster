# CLUSTER data with Conos

Contact: Edwin Juárez <ejuarez@ucsd.edu>, Anthony Castanza <acastanza@ucsd.edu>
>[Link to Anthony's Notebook]

This is step 2 of 3 in the Conos pipeline. This module will read single cell data (e.g., count files) from different datasets and project each of those datasets into their own PCA space.

>[Documentation incomplete]

More details in the original package: https://github.com/hms-dbmi/conos

The module ends by saving some variables to file:
```
# Save an object to a file
saveRDS(list(con=con,runleiden=runleiden,runwalktrap=runwalktrap), "conos_object.rds")
print('saved conos_object.rds')
```
