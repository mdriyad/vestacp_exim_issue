# vestacp_exim_issue

-----------------------------------------
Problem 01
-----------------------------------------

after upgrading to the newest epel release exim-4-94-1.el7 exim stops working and starts complaining in the log.

Sending email:
sender verify defer for <xxxx@domain.com>: failed to expand "${extract{1}{:}{${lookup{$local_part@$domain}lsearch{/etc/exim/domains/$domain/aliases}}}}": NULL

Receiving email:
2020-06-18 11:47:08 Tainted filename for search: '/etc/exim/domains/domain.com/aliases'
2020-06-18 11:47:08 H=stp.vestacp.com [188.226.163.96] X=TLS1.2:DHE-RSA-AES128-SHA:128 CV=no F=<forum@stp.vestacp.com> temporarily rejected RCPT <xxxx@domain.com>: failed to expand "${extract{1}{:}{${lookup{$local_part@$domain}lsearch{/etc/exim/domains/$domain/aliases}}}}": NULL


-----------------------------------------
Solution
-----------------------------------------

If you want to downgrade on CentOS 7 and get back the working version exim-4.93-3.el7.x86_64.rpm do the following:

wget https://ca1.dynanode.net/exim-4.93-3.el7.x86_64.rpm
rpm -Uvh --oldpackage exim-4.93-3.el7.x86_64.rpm



-----------------------------------------
Problem 02
-----------------------------------------

DMARC failure to load tld list '/usr/share/publicsuffix/public_suffix_list.dat': No such file or directory

-----------------------------------------
Solution
-----------------------------------------

This is caused by bug https://bugzilla.redhat.com/show_bug.cgi?id=1836274

A solution would be to do the following:

mkdir /usr/share/publicsuffix
cd /usr/share/publicsuffix
wget https://publicsuffix.org/list/public_suffix_list.dat
