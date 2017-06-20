You can use the freely available Let's Encrypt to provide encryption for your Uplogix Control Center's web interface.

# Requirements

Connection to the INternet

# Prepare System

Log into the Control Center as emsadmin and become root.

## Check /etc/resolv.conf

If not already configured, add a nameserver to resolv.conf.



Use yum to install git.

cd /etc/yum.repos.d
vi CentOS-Base.repo
yum install git-all

```
Installing:
 git-all                            noarch                 1.7.1-4.el6_7.1                     base                     16 k
Installing for dependencies:
 alsa-lib                           x86_64                 1.1.0-4.el6                         base                    389 k
 apr                                x86_64                 1.3.9-5.el6_2                       base                    123 k
 apr-util                           x86_64                 1.3.9-3.el6_0.1                     base                     87 k
 cvsps                              x86_64                 2.2-0.6.b1.el6                      base                     56 k
 emacs-common                       x86_64                 1:23.1-28.el6                       base                     18 M
 emacs-git                          noarch                 1.7.1-4.el6_7.1                     base                     40 k
 emacs-nox                          x86_64                 1:23.1-28.el6                       base                    1.9 M
 fontconfig                         x86_64                 2.8.0-5.el6                         base                    186 k
 freetype                           x86_64                 2.3.11-17.el6                       base                    361 k
 git                                x86_64                 1.7.1-4.el6_7.1                     base                    4.6 M
 git-cvs                            noarch                 1.7.1-4.el6_7.1                     base                     84 k
 git-email                          noarch                 1.7.1-4.el6_7.1                     base                     41 k
 git-gui                            noarch                 1.7.1-4.el6_7.1                     base                    216 k
 git-svn                            noarch                 1.7.1-4.el6_7.1                     base                     95 k
 gitk                               noarch                 1.7.1-4.el6_7.1                     base                    132 k
 gnutls                             x86_64                 2.8.5-19.el6_7                      base                    347 k
 libX11                             x86_64                 1.6.3-2.el6                         base                    586 k
 libXau                             x86_64                 1.0.6-4.el6                         base                     24 k
 libXft                             x86_64                 2.3.2-1.el6                         base                     55 k
 libXrender                         x86_64                 0.9.8-2.1.el6_8.1                   updates                  24 k
 libproxy                           x86_64                 0.3.0-10.el6                        base                     39 k
 libproxy-bin                       x86_64                 0.3.0-10.el6                        base                    9.0 k
 libproxy-python                    x86_64                 0.3.0-10.el6                        base                    9.1 k
 libxcb                             x86_64                 1.11-2.el6                          base                    142 k
 neon                               x86_64                 0.29.3-3.el6_4                      base                    119 k
 pakchois                           x86_64                 0.4-3.2.el6                         base                     21 k
 perl-Authen-SASL                   noarch                 2.13-3.el6                          base                     52 k
 perl-DBI                           x86_64                 1.609-4.el6                         base                    705 k
 perl-Digest-HMAC                   noarch                 1.01-22.el6                         base                     22 k
 perl-Digest-SHA1                   x86_64                 2.12-2.el6                          base                     49 k
 perl-Error                         noarch                 1:0.17015-4.el6                     base                     29 k
 perl-GSSAPI                        x86_64                 0.26-6.el6                          base                     64 k
 perl-Git                           noarch                 1.7.1-4.el6_7.1                     base                     28 k
 perl-IO-Socket-SSL                 noarch                 1.31-3.el6_8.2                      updates                  70 k
 perl-Net-LibIDN                    x86_64                 0.12-3.el6                          base                     35 k
 perl-Net-SMTP-SSL                  noarch                 1.01-4.el6                          base                    8.1 k
 perl-Net-SSLeay                    x86_64                 1.35-10.el6_8.1                     updates                 174 k
 perl-TermReadKey                   x86_64                 2.30-13.el6                         base                     31 k
 perl-URI                           noarch                 1.40-2.el6                          base                    117 k
 subversion                         x86_64                 1.6.11-15.el6_7                     base                    2.3 M
 subversion-perl                    x86_64                 1.6.11-15.el6_7                     base                    797 k
 tcl                                x86_64                 1:8.5.7-6.el6                       base                    1.9 M
 tk                                 x86_64                 1:8.5.7-5.el6                       base                    1.4 M

```

cd to /root
Connect to your server via SSH.
Clone the Let's Encrypt program from Git:
sudo git clone https://github.com/letsencrypt/letsencrypt
Move into the letsencrypt directory:
cd letsencrypt
Install the help files from Let's Encrypt:
./letsencrypt-auto --help

