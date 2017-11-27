knime
=====

Knime provided via a Singularity container.

This is a proof of concept container packaging.
Please go to http://www.knime.com/downloads and complete the registration/EULA.

- Ubuntu Trusty
- Knime installed in /opt (http://www.knime.com) 
- This version does not include the "all free extensions", as the upstream linux package was not avail.
- Include Firefox

Getting and running this knime container:

::

	singularity pull shub://tin6150/knime:master
	singularity run -B /run knime.img 

Note that $HOME is also expected to be bindmounted, so that your knime workspace can be created under it.


Creating containers (if not using Singularity Hub):

::

	Singularity=/opt/singularity/2.3/bin/singularity
	sudo    $Singularity create --size 1900 knime.img    # need 5400 for knime with full extensions
	sudo -E $Singularity bootstrap knime.img Singularity | tee sing_log.txt 2>&1 


Space utilization:

- 1900 MB enough to hold download of knime regular version and uncompress it
	- removing the .tar.gz would save ~400 MB
- 5350 MB needed to hold download and hold the expanded files.
	- removing the .tar.gz would save 1905 MB

  
Ref:

- https://github.com/tin6150/singhub/ubuntu_knime.def
- https://singularity-hub.org/collections/305
-
- https://singularity-hub.org/containers/1898/      # inspiration for -B /run etc.  Thx Tru!!
