"What's up?" is a web application that is able to create a list of astronomical objects
that you can observe from your location.

BACKGROUND
Amateur astronomy has been an endeavour experienced by many people across the centuries, and
by people around the world. While astronomy is one of the oldest sciences in the world, it was
only in the past few decades when it gained popularity among amateurs, enabling the common man
on the street to purchase good quality telescopes.

The astronomical objects that can be seen, or indeed positioned well enough to be seen, varies
depending on geographical location around the world. For instance, the farther North one goes,
the less likely one is able to view objects in the Southern sky. Indeed, there are some objects
so far in the Southern sky, that it will never rise above the horizon in the northern hemisphere.

Despite not being able to access the entirety of the night sky from any single location on Earth
(although those at the equator arguably get to see the most at a go), there are certainly still
a large number of things one can see, no matter where he or she is on the planet.

This web application is therefore able to extract the viewer's geographical coordinates, query a
database, and create a ranked observing list of the brightest objects that can be seen from that
very location.


USAGE AND MECHANISM
Simply by accessing the site, the javascript code automatically logs your current geographical
coordinates, and submits it in the background into a flask application. This is achieved by using
creating a hidden html form, which javascript automatically fills in with the geographical coordinates
and submits as a "POST" request to flask. While flask is working in the background, the page displays
a loading message, and shows the user's coordinates if successful.

Within python/flask, the submitted geographical coordinates will be matched against a database
of nearly 50,000 astronomical objects. This database was acquired from the Saguaro Astronomy
Club (SAC), at https://www.saguaroastro.org/sac-downloads/

The data, in excel form, was then converted into an .db file. The celestial coordinates where then
parsed into floating point values, which could then be applied alongside the user's geographical
coordinates calculations in the python script.

Based on the location of the user, objects that rise at least 20 degrees above the horizon will then
be filtered. Additionally, only objects that are decently bright enough (Magnitude <7) are displayed.

The extracted list/dictionary in python is then converted into a pandas dataframe, where the results
are sorted in decreasing levels of brightness (i.e. increasing magnitude).

This is then passed as an output into the html file using JINJA, which creates the final user-side
webpage in a tabular format.
