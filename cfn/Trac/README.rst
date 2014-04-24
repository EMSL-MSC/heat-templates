First time use, launch Trac-Init.yaml, then delete it when successful. This will create a Trac volume.

You may launch Trac.yaml for every Trac server you wish manually.

Alternately, copy Trac-InstanceExample.yaml to your own repository and change the parameters to match your settings so you can easily relaunch your Trac server.

Once you are up and running some instructions for talking to the instance.

If you have not loaded custom certs into the instance, you may checkout the git repository like:
git clone -c http.sslVerify=false https://<your instance ip>/<your trac name>.git

After checking out the repository for the very first time, you must push your first commit like:
git push --set-upstream origin master

