# Device Edge Image Builder
This role provides a means to configure a EL system with osbuild-composer that
can build and update Device Edge ostree images. The images can be retrieved from the
local webserver.

After running this role you have a system that can manage ostree images. You will still need:

  * A DHCP/TFTP setup that will enable PXEbooting on the target devices
  * A blueprint for making images

Further documentation on how to work with Device Edge can be found here: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/composing_installing_and_managing_rhel_for_edge_images/introducing-rhel-for-edge-images_composing-installing-managing-rhel-for-edge-images

The role supports defining extra repositories which can be hosted in a local Satellite server.

When you have compiled a blueprint, you can publish the resulting artifact in ''/var/www/html/<image>'', which will make it available.

Please see defaults/main.yml for more details.
