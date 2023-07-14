API
===
This section provides detailed documentation for the classes and methods available in the GIS package.

GeographicPoint
---------------

Represents a geographic point with latitude, longitude, and elevation coordinates.

.. class:: GeographicPoint

   .. method:: __init__(latitude, longitude, elevation)

      Initializes a new instance of the GeographicPoint class with the given longitude, latitude, and elevation coordinates.

      :param latitude: Floating-point value within the range -90 to 90, representing the latitude.
      :type latitude: float
      :param longitude: Floating-point value within the range -180 to 180, representing the longitude.
      :type longitude: float
      :param elevation: Value in meters above the datum (≈ sea level). Use elevation = 0 for 2D points. This will allow for 2D points to be computed with 3D points.
      :type elevation: float
      :returns: None
      :throws ValueError: If latitude or longitude is outside the valid range.

   .. method:: setLatitude(latitude)

      Changes the latitude to the new latitude.

      :param latitude: Floating-point value within the range -90 to 90, representing the new latitude.
      :type latitude: float
      :returns: None
      :throws ValueError: If latitude is outside the valid range.

   .. method:: setLongitude(longitude)

      Changes the longitude to the new longitude.

      :param longitude: Floating-point value within the range -180 to 180, representing the new longitude.
      :type longitude: float
      :returns: None
      :throws ValueError: If longitude is outside the valid range.

   .. method:: setElevation(elevation)

      Changes the elevation to the new elevation.

      :param elevation: Value in meters above the datum (≈ sea level). Use elevation = 0 for 2D points.
      :type elevation: float
      :returns: None
   
   .. method:: setTimezone(timezone)

      Sets the timezone for the geographic point.

      :param timezone: A string representing the timezone of the geographic point.
      :type timezone: str
      :returns: None

   .. method:: getTimezone()

      Gets the timezone of the geographic point.

      :returns: The timezone of the geographic point.
      :rtype: str


Polygon
-------

Represents a polygon defined by a collection of points.

.. class:: Polygon

   .. method:: __init__(points)

      Initializes a new instance of the Polygon class with the given collection of points.

      :param points: List of points representing the vertices of the polygon.
      :type points: List[GeographicPoint]
      :returns: None

   .. method:: contains(point)

      Determines if a point is inside the polygon.

      :param point: Point of the geographical coordinates.
      :type point: GeographicPoint
      :returns: True if the point is inside the polygon, False otherwise.
      :rtype: bool

   .. method:: polygonRemove(point)

      Removes the given point from the polygon.

      :param point: Geographic point to be removed.
      :type points: GeographicPoint
      :returns: None

   .. method:: polygonAdd(point)

      Adds the given point to the polygon.

      :param point: Geographic point to be added.
      :type points: GeographicPoint
      :returns: None

   .. method:: getArea()

      Calculates the area of the polygon.

      :returns: Area of the polygon in square meters.
      :rtype: float

   .. method:: getPerimeter()

      Calculates the perimeter of the polygon.

      :returns: Perimeter of the polygon in meters.
      :rtype: float

   .. method:: isConvex()

      Checks if the polygon is convex.

      :returns: True if the polygon is convex, False otherwise.
      :rtype: bool


Track
-----

Represents a track or path defined by a collection of points.

.. class:: Track

   .. method:: __init__(points)

      Initializes a new instance of the Track class with the given collection of points.

      :param points: List of points representing the track or path.
      :type points: List[GeographicPoint]
      :returns: None

   .. method:: length()

      Calculates the length of the track.

      :returns: Length of the track in meters.
      :rtype: float

   .. method:: trackRemove(point)

      Removes the given point from the track.

      :param point: Geographic point to be removed.
      :type points: GeographicPoint
      :returns: None

   .. method:: trackAdd(point)

      Adds the given point to the track.

      :param point: Geographic point to be added.
      :type points: GeographicPoint
      :returns: None


GPXParser
---------

Parses GPX files and constructs data structures.

.. class:: GPXParser

   .. method:: __init__(file_path)

      Initializes a new instance of the GPXParser class with the given GPX file path.

      :param file_path: Path to the GPX file.
      :type file_path: str
      :returns: None
      :throws FileNotFoundError: If the specified GPX file does not exist.

   .. method:: parse()

      Parses the GPX file and returns the constructed data structure.

      :returns: A data structure representing the GPX file.
      :rtype: Tuple[List[GeographicPoint], str]
      :throws ValueError: If the GPX file is invalid or has missing data.

   .. method:: getTrackNames()

      Retrieves the names of all tracks in the GPX file.

      :returns: List of names of all the tracks.
      :rtype: List[str]

   .. method:: getTrackPoints(track_name)

      Retrieves the points of a specific track in the GPX file.

      :param track_name: Name of the track to retrieve points for.
      :type track_name: str
      :returns: Points of the specific track.
      :rtype: Track


Functions
---------

.. py:function:: getDistance(startPoint, endPoint)

      Gets the distance from startPoint to endPoint.

      :param startPoint: The start point.
      :type startPoint: GeographicPoint
      :param endPoint: The end point.
      :type startPoint: GeographicPoint
      :returns: Distance in meters.
      :rtype: float

.. py:function:: farthestPoint(pointsCollection)

      Gets the farthest points in the collection of points.

      :param pointsCollection: List of all points.
      :type pointsCollection: List[GeographicPoint]
      :returns: An List of 2 points.
      :rtype: List[GeographicPoint]

.. py:function:: shortestPoint(pointsCollection)

      Gets the shortest points in the collection of points.

      :param pointsCollection: List of all points.
      :type pointsCollection: List[GeographicPoint]
      :returns: An List of 2 points.
      :rtype: List[GeographicPoint]

.. py:function:: getAllPointsIn(borderPoints)

      Using the List of the borderPoints, it returns points within the border.

      :param borderPoints: List of all points.
      :type borderPoints: List[GeographicPoint]
      :returns: An List of points within the border points.
      :rtype: List[GeographicPoint]

.. py:function:: averagePoint(points)

   Calculates the average point from a collection of points.

   :param points: List of points.
   :type points: List[GeographicPoint]
   :returns: The average point.
   :rtype: GeographicPoint

.. py:function:: isClockwise(points)

   Determines if a sequence of points represents a clockwise or counterclockwise polygon.

   :param points: List of points representing the polygon vertices.
   :type points: List[GeographicPoint]
   :returns: True if the points form a clockwise polygon, False otherwise.
   :rtype: bool

.. py:function:: averageDistance(points)

   Calculates the average distance between points from a collection of points.

   :param points: List of points.
   :type points: List[GeographicPoint]
   :returns: The average distance in meters.
   :rtype: GeographicPoint

Usage Examples
--------------

Example 1: Finding the Farthest Apart Points
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's say we have a collection of 2D geographic points represented by a list:

.. code-block:: python

   points_collection = [
       GeographicPoint(45.123, -78.456, 0),  # Point A
       GeographicPoint(48.789, -80.234, 0),  # Point B
       GeographicPoint(46.567, -79.012, 0),  # Point C
       # Add more points as needed
   ]

To find the two points that are farthest apart from each other, we can use the `farthestPoint` function:

.. code-block:: python

   farthest_points = farthestPoint(points_collection)

The `farthest_points` variable will now hold a List containing the two points that are farthest apart.

The distance between the two farthest points can be calculated using the `getDistance` function:

.. code-block:: python

   distance = getDistance(farthest_points[0], farthest_points[1])

The variable `distance` will now hold the distance in meters between the two farthest points.



Example 2: Using Wikipedia Articles to Find Points in Canada
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Assuming we have the following data:

1. A collection of 2D points representing the borders of Canada, stored in the `canada_borders` list.
2. A collection of geographic coordinates of Wikipedia articles, stored in the `wikipedia_articles` list.

To find all Wikipedia articles referencing a point within Canada, we can follow these steps:

1. Create a `Polygon` object using the `canada_borders` list of points:

.. code-block:: python

   canada_polygon = Polygon(canada_borders)

2. Iterate through the `wikipedia_articles` list and check if each article's location is within Canada:

.. code-block:: python

   wikipedia_articles_points = []
   for article in wikipedia_articles:
       if canada_polygon.contains(article):
           wikipedia_articles_points.append(article)

Now, the `wikipedia_articles_points` list will contain all Wikipedia articles whose locations fall within the borders of Canada.



Example 3: Drawing User's Path on Google Maps from GPX Data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Assuming the user's GPS data is recorded in a GPX file named "user_path.gpx."

To draw the user's path on Google Maps, we need to follow these steps:

1. Parse the GPX file using the `GPXParser` class:

.. code-block:: python

   gpx_parser = GPXParser("user_path.gpx")
   user_track_points, track_name = gpx_parser.parse()

2. Create a `Track` object using the `user_track_points` list:

.. code-block:: python

   user_track = Track(user_track_points)

3. Calculate the length of the user's track:

.. code-block:: python

   track_length = user_track.length()

4. Now, we have the user's track data, and we can use this data to draw the path on Google Maps.

Note: To draw the path on Google Maps, you'll need to use the Google Maps API or other mapping libraries that support drawing paths from geographic data.


In the given documentation, the methods/functions do not specify any explicit "throws" statements. Therefore, it can be assumed that these methods/functions do not throw any specific exceptions or errors and rely on the built-in Python exceptions when needed. However, it's always a good practice to handle exceptions appropriately when using these methods/functions in a real application to avoid unexpected behavior.
