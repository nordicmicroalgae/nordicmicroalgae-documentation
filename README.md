# Nordic Microalgae

Welcome to the Nordic Microalgae project.

The web site is a source of information about microalgae and related organisms in the Nordic area, i.e. the Baltic Sea, the North East Atlantic and lakes, rivers and streams in the area.  This site is of use for science, education, environmental monitoring etc. The content of the site is mainly supplied by the users.

The web site can be found here: http://nordicmicroalgae.org/ 

The Nordic microalgae web application contains a taxonomic backbone, species sheets and images supplied by registered and approved contributors. Images can be searced for in a number of ways to make it easier to find alternatives when working with species identification.

Technically the system is divided into some clearly separated parts:

- A core data layer. 

- A web user interface which also contains CMS (Content Management System) functionality.

- A mobile client.

The data layer is developed in Python and data is stored in a MySql database. There is an API where all data can be read. The API is described here: https://github.com/nordicmicroalgae/nordicmicroalgae-documentation/blob/master/doc/nordicmicroalgae-data-api.md

The web user interface is developed in Drupal with some new modules developed to handle the Nordic Microalgae specific tasks. A separate MySql database is used for Drupal.

The mobile client is a html client working on top of the API.

All source code used in the project is stored in this GitHub organisation: https://github.com/nordicmicroalgae
