Jenkins Google Container Registry Plugin
====================

This plugin provides the credential provider to use Google Cloud Platform Oauth Credentials (provided by the Google Oauth Plugin) to access Google Container Registry. It supports both kinds of credentials provided by Google Oauth Plugin: Google Service Account from metadata as well as Google Service Account from private key.

Your service account will need to have the scope of https://www.googleapis.com/auth/devstorage.read_write or https://www.googleapis.com/auth/devstorage.full_control, and need to have access to your image bucket in Google Container Registry.

Usage
===
First, install Docker Build Step Plugin.

Second, configure your OAuth credentials per instructions from Google OAuth Plugin, using the service account that has read/write access to your Google Container Registry.

Third, install this plugin, then on Jenkins' global configuration page, under "Google Container Registry", set the correct Google Container Registry server address. By default, it is "gcr.io" (Do not include schemes such as "https://").

Fourth, in your Jenkins job, add a build step "Execute Docker Container", and choose either "pull image" or "Push image" as your docker command (other docker commands don't require credentials so they are not relevant to this plugin). Enter image name, tag and registry. In the "Registry Server Address" field, by default you should enter "https://gcr.io". The value in this field should match the value in "Google Container Registry" Server Address field in global configuration, but with the scheme (such as https://) added.

Then, in the "Docker Credential" dropdown, select your account marked as "Google Contaner Registry Account".

Save your configuration and run your job.

Security Warning
===
Docker Build Step Plugin will pass the credentials to Docker server daemon. If the Docker server daemon listens on HTTP port, this will create a security hole because the credentials (not encrypted, only base64 encoded) can be intercepted via the HTTP traffic. This is a problem of Docker itself. Configuring the Docker server daemon to listen on HTTP port is strongly discouraged. When communication to Docker daemon on a remote machine is needed, the traffic can be secured by HTTPS, see Docker's documentation: http://docs.docker.com/articles/https/.

Development
===========

How to build
--------------

	mvn clean verify

Creates the plugin HPI package for use with Jenkins.


License
-------

	(The Apache v2 License)

    Copyright 2015 Google Inc. All Rights Reserved.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
