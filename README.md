This is a library file for Cfengine3. This library has been tested on cfengine-community 3.5.1-1 and on debian based systems; Including Wheezy (7) and Ubuntu 12.04 LTS.

The base content of this library was converted from pip.cf by swesterveld.

Usage:

In your cfengine3's promises.cf place the location of your gem.cf library in the inputs section as exampled below.

      ###############################################################################
      #
      #   promises.cf - Basic Policy for Community
      #
      ###############################################################################

      body common control

      {

      bundlesequence => {
         # Global bundle
            "global",

         # Run Policy Update
            "update",

                 # Common bundles first for best practice
                    "def",

        };
        
      inputs => {
      
            # COPBL/Custom libraries
            "cfengine_stdlib.cf",
            "gem.cf",
      };
      

For Agent usage:

      bundle agent example
      {
      vars:
              "fluent_gem_pkgs" slist => {
                "fluent-plugin-forest",
            };
              "gem_pkgs" slist => {
                "fpm",
            };
      
      packages:
              
             any::
             "$(fluent_gem_pkgs)"
                  package_policy => "addupdate",
                  package_method => fluent_gem_pkg;
             
             any::
             "$(gem_pkgs)"
                  package_policy => "addupdate",
                  package_method => gem_pkg;
      }
      
TODO:
=====

Add better regex for versions
Patches welcome!

