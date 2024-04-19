# Device Edge Image Builder
This role provides a means to configure a EL system with osbuild-composer that
can build and update Device Edge ostree images. The images can be retrieved from the
local webserver. If desired, this role can also provide a simple DHCP/TFTP setup to
do PXEboot deployments of the images.

After running this role you have a system that can manage ostree images. You will still need a blueprint for making images. The role supports defining extra repositories which can be hosted in a local Satellite server.

Further documentation on how to work with Device Edge can be found here: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/composing_installing_and_managing_rhel_for_edge_images/introducing-rhel-for-edge-images_composing-installing-managing-rhel-for-edge-images

NOTE: This role only implements the 'toolchain' required for managing Device Edge images, building the images themselves is managed in the 'edge_compose_blueprint' role.

## Deployment server
This role can be configured to configure a simple DHCP/TFTP deployment setup that will allow for PXEbooting target systems. This deployment setup will:

  * Use a DHCP range from <subnet>.20 to <subnet>.50
  * Assume it's the only DHCP server in the network

Please see defaults/main.yml for more details which can be configured for the deployment server. Note that this role will not configure a PXEboot menu if no blueprints are built with it.

## Building images
This role can be configured to build and publish all blueprints found in ''/etc/osbuild-composer/blueprints''. For this mechanism to work you need to place the following files:

  * <image>.toml: the osbuild-composer blueprint
  * <image>.ks: the kickstart file which will be used to deploy the image

If these files are both present, the role will import the blueprint to osbuild-composer, build the image and publish the artifacts in ''/var/www/html/<image>'', after which is can be deployed to target systems.

It will also generate a PXEboot menu for the images it has built, if you do not configure the role to process blueprints, it will not generate a menu.

## Distro versions
The image builder is capable of building multiple versions of the Device Edge OS, but when running Satellite, you must ensure that the server has acccess to the repositories required for it.
