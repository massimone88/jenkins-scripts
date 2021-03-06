# jenkins-scripts

Miscellaneous scripts for jenkins


maven-to-freestyle.groovy
-----------------------
* Jenkins groovy script to convert Maven projects that use JDK 1.6 to freestyle projects. 
* Jenkins > 1.609 no longer supports JDK 1.6 and neither do Maven projects - in fact, all Maven projects run on whatever JDK version the server runs. 
* Does not use the REST API, works directly with jenkins by retrieving and modifying job XML live

What it does:
* Moves old jobs out of the way and creates new ones using the old name
* Keeps the XML unchanged except:
  * moves all prebuilders to builders (unchanged)
  * moves maven main step to builders, losing some settings that are not supported in a maven build step.
  * moves all postbuilders to builders (unchanged)
  * keeps publishers and everything else unchanged.

To use:

* Create a job with an "Execute ***System*** Groovy Script" step.  Paste in the code or use git directly.
* Job must run on master (if you remove file archiving you can run it on slaves)
* Read the top of the comments in script for build parameters
* Run in DRY_RUN mode and review workspace xml (old and new).  If changes look good, run for real.
