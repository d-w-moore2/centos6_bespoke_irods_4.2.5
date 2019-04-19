# centos6_bespoke_irods_4.2.5

Compiling  & installing iRODS 4.2.5 from source - for Hydroshare 4/18/2019

starting from Centos 6.x Minimal install

   - (1) upgrade Centos to at least 6.10
      * `yum clean all`
      * `yum update`
      * confirm `/etc/redhat-release` contains  (>=) Centos (Final) 6.10
      * install wget , gcc-c++, git , openssl-devel, pam-devel, unixODBC-devel , rpm-build

   - (2) Use git to clone irods/irods, irods/irods_client_icommands
          ( git checkout 4.2.5)
         also: irods/irods_resource_plugin_s3 (git checkout 4-2-stable)

   - (3)disable selinux ; edit /etc/selinux/config to read disabled, in place of  enforcing, then reboot (sestatus should report  "disabled". 

   - (4) set libarchive3.3.2 -> libarchive3.1.2 in CMakeLists.txt , root dir of irods/irods

   - (5) install irods externals (from avro to zeromq4, and cmake) as listed in:
         `https://github.com/irods/irods/blob/4.2.5/irods_consortium_continuous_integration_build_hook.py`

         also `sudo yum install irods-externals-libs3a30e55e8-0 irods-externals-libs3f6a2098e-0`

   - (6) PATH=/opt/irods-externals/cmake3.5.2-0/bin/:$PATH
   - (7) install EPEL
   ```
   # wget http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
   # rpm -ivh epel-release-6-8.noarch.rpm
   ```
   - (8) compile as normal

   - (9) Note warnings
   ```
   CPackRPM:Debug: Adding /usr/sbin to builtin omit list.
CPackRPM: Will use GENERATED spec file: /home/danielm/build_irods/_CPack_Packages/Linux/RPM/SPECS/irods-runtime.spec
CMake Warning (dev) at /opt/irods-externals/cmake3.5.2-0/share/cmake-3.5/Modules/CPackRPM.cmake:667 (list):
  Policy CMP0007 is not set: list command no longer ignores empty elements.
  Run "cmake --help-policy CMP0007" for policy details.  Use the cmake_policy
  command to set the policy and suppress this warning.  List has value = [
  ;].
Call Stack (most recent call first):
  /opt/irods-externals/cmake3.5.2-0/share/cmake-3.5/Modules/CPackRPM.cmake:1505 (cpack_rpm_prepare_content_list)
  /opt/irods-externals/cmake3.5.2-0/share/cmake-3.5/Modules/CPackRPM.cmake:1787 (cpack_rpm_generate_package)
  
This warning is for project developers.  Use -Wno-dev to suppress it.


   ```
   
   
================================================
 
