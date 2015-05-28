---
title: Oracle (RDS) + CentOS 5.8 (EC2) + Python (cx_Oracle)
author: ajordens
layout: post
permalink: /2012/07/rds-oracle-centos-5-8-ec2-python/
categories:
  - Database
  - General Discussions
---
<!--?xml version="1.0" encoding="UTF-8" standalone="no"?-->

**For anyone looking to have Python (CentOS 5.8) connect to an Oracle instance (RDS):**

$ yum install python26 python26-devel (*I was using a Rightscale instance that already had the EPEL repository loaded, otherwise see: <http://fedoraproject.org/wiki/EPEL>*)

<span style="font-size: 12px;"><span>$ wget </span><span><a href="http://pypi.python.org/packages/2.6/s/setuptools/setuptools-0.6c11-py2.6.egg#md5=bfa92100bd772d5a213eedd356d64086">http://pypi.python.org/packages/2.6/s/setuptools/setuptools-0.6c11-py2.6.egg#md5=bfa92100bd772d5a213eedd356d64086</a></span></span>

<span style="font-size: 12px;">$ sh setuptools-0.6c11-py2.6.egg</span>

<span style="font-size: 12px;">$ easy_install-2.6 pip</span>

<span style="font-size: 12px;">$ pip-2.6 install virtualenvwrapper</span>

<span style="text-decoration: underline; font-size: 12px;"><span style="text-decoration: underline; font-size: 12px;"><strong><br /></strong></span></span>

<span style="text-decoration: underline; font-size: 12px;"><span style="text-decoration: underline; font-size: 12px;"><strong>Add to /etc/profile</strong></span></span>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.6</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">. /usr/bin/virtualenvwrapper.sh</span>
</div>

<div style="font-family: Arial;">
   
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">export ORACLE_HOME=/opt/oracle/instantclient_11_2</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">export ORACLE_BASE=/opt/oracle/instantclient_11_2</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">export TNS_ADMIN=/opt/oracle/instantclient_11_2</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">export ORACLE_HOME=/opt/oracle/instantclient_11_2</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">export LD_LIBRARY_PATH=/opt/oracle/instantclient_11_2</span>
</div>

<div style="font-family: Arial;">
   
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">$ mkdir -p /opt/oracle</span>
</div>

<div style="font-family: Arial;">
   
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">$ unzip instantclient-basic-linux.x64-11.2.0.3.0.zip -d /opt/oracle</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;"><br /></span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">$ cd /opt/oracle/instant*</span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;"><br /></span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">$ ln -s <a href="http://libclntsh.so/">libclntsh.so</a>.11.1 libclntsh.so</span>
</div>

<div style="font-family: Arial;">
   
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">$ rpm -i <a href="http://prdownloads.sourceforge.net/cx-oracle/cx_Oracle-5.1.2-11g-py26-1.x86_64.rpm?download">http://prdownloads.sourceforge.net/cx-oracle/cx_Oracle-5.1.2-11g-py26-1.x86_64.rpm?download</a></span>
</div>

<div style="font-family: Arial;">
  <span style="font-size: 12px;">$ mkvirtualenv oracle &#8211;system-site-packages</span>
</div>

<span style="text-decoration: underline; font-size: 12px;"><strong><br /></strong></span>

<span style="text-decoration: underline; font-size: 12px;"><strong>Create /opt/oracle/instantclient_11_2/tnsnames.ora</strong></span>

TOYBOX =  
(DESCRIPTION =  
(ADDRESS_LIST =  
(ADDRESS = (PROTOCOL = TCP)(HOST = X.Y.us-east-1.rds.amazonaws.com)(PORT = 1521))  
)  
(CONNECT_DATA =  
(SERVICE_NAME = ORCL)  
)  
)

 

<span style="text-decoration: underline; font-size: 12px;"><strong>Connect via Python</strong></span>

(oracle)[root@domU-12-31-39-16-36-60 python-connect]# python2.6

Python 2.6.8 (unknown, Apr 12 2012, 20:59:36)   
[GCC 4.1.2 20080704 (Red Hat 4.1.2-52)] on linux2  
Type &#8220;help&#8221;, &#8220;copyright&#8221;, &#8220;credits&#8221; or &#8220;license&#8221; for more information.  
>>> import cx_Oracle  
>>>   
>>> connection = cx_Oracle.connect(&#8216;USERNAME/PASSWORD@TOYBOX&#8217;)  
>>> cursor = connection.cursor()  
>>> cursor.execute(&#8220;SELECT count(*) FROM sys.dba\_tab\_privs WHERE grantee=&#8217;PUBLIC'&#8221;)  
<\_\_builtin\_\_.OracleCursor on <cx_Oracle.Connection to ajordens@TOYBOX>>  
>>> count = cursor.fetchall()\[0\]\[0\]  
>>>   
>>> print count  
2494  
>>>   
>>> cursor.close()  
>>> connection.close()