# Cosmoteka Tutorials
![](https://raw.githubusercontent.com/JaimeRZP/Cosmoteka_tutorials/master/docs/src/assets/cosmoteka_logo.png)
<p align="center"> Tutorials for the Cosmoteka mappers </p>

## Mappers
In order to understand, how the `mapper` modules compute the `NaMaster` fields we can look the `mapper_base.py`, the mapper module which defines the parent class for all other mappers inside Cosmoteka. As the parent class, `mapper_base` defines a series of default methods which are then overwritten by the child mappers to perform the data processing specific to each data set. Moreover, it also defines common methods to each mapper. The most important of these methods is `get_nmt_field` which projects the catalogs into `NaMaster` fields. Inside `get_nmt_field`, the signal map and mask of each mapper are computed according to the specifc methods of the children mappers. Then, the signal map and mask as well as other mapper specific quantities (data beam, contaminants,... etc) are passed on to `NaMaster` to compute the final field.
