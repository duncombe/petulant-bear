petulant-bear
=============
COPYRIGHT 2013 RPS ASA


This file is part of  Petulant Bear.


    Petulant Bear is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.


    Petulant Bear is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.


    You should have received a copy of the GNU General Public License
    along with Petulant Bear.  If not, see <http://www.gnu.org/licenses/>.

Petulant (Adjective - of a person or their manner): 
* Childishly sulky or bad-tempered.

Bear (Verb  - used with object):
* To hold up; support: to bear the weight of the roof.

Description
===========
Presents etree interface to netcdf4-python objects using NCML data model


This library attempts to provide a bridge to support uniform metadata operation in python on XML and NetCDF files using the LXML interface. As the name suggests, while a serious effort has been made to provide a clean and consistent interface which will support the weight of metadata management the library may be a bit cranky if you try to do things that don't make sense. So far I have only tried to support the key operations required for the wicken library.

Good luck

Examples
========
Creating NCML from a nc file:
    from petulantbear.netcdf2ncml import *
    
    fname = '/Users/dstuebe/code/petulant-bear/test_data/test.nc'
    str_out = ''
    with Dataset(fname) as ds:
        str_out = dataset2ncml(ds, url="file:"+fname)
    print len(str_out)

    with open('test_data/test.xml','w') as output: 
        output.write(str_out)



Working with an NC file as a lxml object:

    from petulantbear.netcdf_etree import *
    fname = 'profile_shore.nc'
    ds = Dataset(fname,'a')
    root = parse_nc_dataset_as_etree(ds)
        
    dim = root[0]
    att.attrib # will show the xml attributes of this dimension
    att.attrib['name'] = 'foobar'
    
