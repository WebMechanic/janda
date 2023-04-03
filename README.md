
Original version of this project was two commits forward - modifications and imporovements from WebMechanic were "manually merged" into the most recent version of the original project so as not to lose the changes which had been made via two recent commits to the original project.
Moving forward, implementation of @use and @forward directives (as demonstrated bt WebMechanic) will be carried out within the recently added _links.scss partitial, and any future additional partials. 



----
> The Repo was created for educational purposes for a 3rd party and will be removed shortly.
----

# r1
 r1

april 2: 
TO COMPILE SCSS TO CSS (STYLE.SCSS --> STYLE.CSS)
using Windows Powershell or CMD.exe with command...

    sass --watch scss:css

Requires Dart Sass from https://github.com/sass/dart-sass/releases/tag/1.60.0 inside `PATH`

To make sure Sass tells about deprecated features run

    sass --future-deprecation import --watch scss:css
