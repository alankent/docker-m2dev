Magento 2 Development Environment
=================================

This is the Dockerfile behind the alankent/m2dev Docker image.
This image contains Apache, PHP 6, Gulp and other similar development
tools preinstall, but no Magento site.

If `SAMBA_START=1` is set as an environment variable when the
container is started, a Samba server is launched to give remote
access to the files in the container.

The following is a convenient `docker-composer.yml` file for
use with this image that specifies all the port numbers to open
up by default. Note this mounts your ~/.composer directory inside
the container, so it can access your ~/.composer/auth.json file
for credentials to the Magento composer repository.

    m2dev:
      image: alankent/m2dev
      ports:
        - "80:80"
        - "3000:3000"
        - "3001:3001"
        - "135:135"
        - "139:139"
        - "445:445"
        - "2222:22"
      environment:
        - SAMBA_START=1
      volumes:
        - ~/.composer:/home/magento/.composer

To start, use

    docker-compose up -d

Alternatively you can do it all by command line switches instead.

    docker run -d -i -t -p 80:80 -p 3000:3000 -p 3001:3001 -p 2222:22 -p 445:445 -p 139:139 -p 135:135 -e SAMBA_START=1 --name gsd alankent/m2dev

Once the container is running, from Windows you can connect using (replace
192.168.99.100 with the IP address used by Docker on your machine)

    net use M: \\192.168.99.100\magento

To create a new project, either use TODO (composer create-project or
git clone an existing repo)..Z
