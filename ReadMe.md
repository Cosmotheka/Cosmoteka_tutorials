# Cosmoteka Tutorials
![](https://raw.githubusercontent.com/JaimeRZP/Cosmoteka_tutorials/master/docs/src/assets/cosmoteka_logo.png)
<p align="center"> Tutorials for the Cosmoteka mappers </p>

## Mappers
The purpose of Cosmoteka's mappers is to compute ```Namaster``` fields from catalogs.
In order to do so Cosmoteka's mappers have to overcome two challenges:
- Be general enough such that they can be inter-operable yet tailor to the catalog's specific needs.
- Manage the large RAM memory usage required to load in and process mordern day catalogs.

Cosmoteka overcomes the first issue by adopting a nested structure. ```MappeBase``` acts as the basis of all other mappers in Cosmoteka. As the parent class, `mapper_base` defines a series of default methods which are then overwritten by the child mappers to perform the data processing specific to each data set. In order to do so, Cosmoteka exploits the Object oriented philosphy of the python language to create a series of mapper classes which are subordinate to one another. A listing of the methods can be found below:

| Function                 | Description                                                                                                                                                    |
| -----------              | :-----------                                                                                                                                                   |
| ```_get_defaults()```    | Reads the configuration file to obtain the desire resolution and coordinates. Initialises the ```NaMaster``` field, signal map, mask and beam as ```None```.   |
| ```_get_rotator()```     | If the ```Mapper``` coordinates are different from the configuration coordinates, creates a ```HealPy```rotator.                                               |
| ```get_signal_map()```   | If the Mapper signal map is not ```None```, returns it. Otherwise, asks ```_get_signal_map()``` to compute it.                                                 |
| ```_get_signal_map()```  | Redirects MapperBase to the specific Mapper method to compute the signal map from the catalog or otherwise.                                                    |
| ```get_mask()```         | If the Mapper mask is not ```None```, returns it. Else, asks ```_get_mask()``` to compute it.                                                                  |
| ```_get_mask()```        | Redirects MapperBase to the specific Mapper method to compute the mask from the catalog or otherwise.                                                          |
| ```get_beam()```         | If the Mapper beam is not ```None```, returns it. Else, asks ```_get_beam()``` to compute it.                                                                  |
| ```_get_beam()```        | Redirects MapperBase to the specific Mapper method to compute the beam from the catalog or otherwise.                                                          |
| ```get_nmt_signal()```   | If the Mapper ```NaMaster``` field is not ```None```, returns it. Else, asks ```_get_nmt_signal()``` to compute it.                                            |
| ```_get_nmt_signal()```  | Calls  ```get_signal_map()```,  ```get_mask()``` and  ```get_beam()``` to obtain the Mapper's signal map, mask and beam respectively. Then it passes them on to  ```Namaster``` to compute the field. |

Concerning the second challenge, Cosmoteka generates a series of rerun files when the mappers are processes for the first time (for a specific resolution and set of coordinates). These reruns files are named following a convention that allows Cosmoteka to fetch them in the future. These files contain the processed ``NaMaster``` field, map signal, mask and beam such that the catalog is not loaded into memory again.
