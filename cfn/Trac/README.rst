First time use, launch Trac-Init.yaml, then delete it when successful. This will create a Trac volume.

You may launch Trac.yaml for every Trac server you wish manually.

Alternately, copy Trac-InstanceExample.yaml to your own repository and change the parameters to match your settings so you can easily relaunch your Trac server.

Once you are up and running some instructions for talking to the instance.

If you have not loaded custom certs into the instance, you may checkout the git repository like:
git clone -c http.sslVerify=false https://<your instance ip>/<your trac name>.git

After checking out the repository for the very first time, you must push your first commit like:
git push --set-upstream origin master


-----------------------------------------------------------------------------------------------------------
Tips and Tricks:

If you do not load a ssl cert into the instance, you may need to work around the self signed cert.

If you are running a git version that supports the -c flag, you can do your initial checkout like:
git clone -c http.sslVerify=false https://<Trac URL>/<reponame>.git

If your git does not suport the -c flag, do the following:
GIT_SSL_NO_VERIFY=true git clone https://<Trac URL>/<reponame>.git
cd <reponame>
cat >> .git/config <<EOF
[http] 
        sslVerify = false
EOF


To download a raw file out of your repo, you can use a url like the following:
https://<Trac URL>/trac/export/HEAD/<filename>

