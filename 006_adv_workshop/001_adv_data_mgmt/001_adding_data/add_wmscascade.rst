.. module:: geoserver.add_wmscascade
   :synopsis: Learn how to add a WMS Cascade Layer.

.. _geoserver.add_wmscascade:

Adding a WMS Cascade Layer
--------------------------

WMS cascading allows to expose layers coming from other WMS servers as if they were local layers. This provides for some interesting advantages:

 * Clients connecting to your SDI need to care about less points of origin, which might be important for high security networks
 * It is now possible to ask for maps in formats not supported by the original server, or to reproject the maps in projections not supported by the original server (GeoServer supports out of the box almost 5000 different coordinate reference systems)
 * It is now possible to mix the layers with local ones to generate print oriented formats such as PDF
 * It is now possible to provide more informations about the layer, such as a better description, more keywords, which will benefit all clients, in particular catalogues harvesting informations from your capabilities document

**Configuration**

The configuration as usage of the cascaded layers follows GeoServer traditional ease of use.

#. Open the web browser and navigate to the GeoServer `Welcome Page <http://localhost:8083/geoserver>`_.

#. Select :guilabel:`Add stores` from the interface. 

   .. figure:: img/geotiff_addstores.png

#. Select :guilabel:`WMS - Cascades a remote Web Map Service` from the set of available Other Data Sources. 

   .. figure:: img/wmscascade_sources.png
   

#. Specify a proper name (as an instance, :file:`geoserver-enterprise`) in the :guilabel:`Data Source Name` field of the interface. 
#. Specify :file:`http://demo1.geo-solutions.it/geoserver-enterprise/ows?service=wms&version=1.1.1&request=GetCapabilities` as the URL of the sample data in the :guilabel:`Capabilities URL` field. 

   .. figure:: img/wmscascade_store.png

#. Click :guilabel:`Save`. 

#. Publish the layer by clicking on the :guilabel:`publish` link near the `GeoSolutions:ne_shaded` layer name. Notice that you can also add more layers later.

   .. figure:: img/wmscascading_publish.png

#. Check the Coordinate Reference Systems and the Bounding Boxes fields are properly set and click on :guilabel:`Save`. 

   .. figure:: img/wmscascade_bbox.png

#. At this point the new WMS Layer is being published with GeoServer. You can use the layer preview to inspect the data.

   .. figure:: img/wmscascading_preview.png
