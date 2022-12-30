# redhat-satellite
<pre>
<b>Executing: foreman-rake upgrade:run</b>
=============================================
Upgrade Step 1/15: katello:correct_repositories. This may take a long while.
=============================================
Upgrade Step 2/15: katello:correct_puppet_environments. This may take a long while.
=============================================
Upgrade Step 3/15: katello:clean_backend_objects. This may take a long while.
0 orphaned consumer id(s) found in candlepin.
Candlepin orphaned consumers: []
0 orphaned consumer id(s) found in pulp.
Pulp orphaned consumers: []
=============================================
Upgrade Step 4/15: katello:upgrades:3.8:clear_checksum_type. =============================================
Upgrade Step 5/15: katello:upgrades:3.10:clear_invalid_repo_credentials. =============================================
Upgrade Step 6/15: katello:upgrades:3.10:update_gpg_key_urls. =============================================
Upgrade Step 7/15: katello:upgrades:3.11:import_yum_metadata. Importing Yum Metadata Files
Failed upgrade task: katello:upgrades:3.11:import_yum_metadata, see logs for more information.
=============================================
Upgrade Step 8/15: katello:upgrades:3.11:update_puppet_repos. =============================================
Upgrade Step 9/15: katello:upgrades:3.11:clear_checksum_type. =============================================
Upgrade Step 10/15: katello:upgrades:3.12:remove_pulp2_notifier. =============================================
Upgrade Step 11/15: katello:upgrades:3.13:republish_deb_metadata. Input file /var/lib/pulp/0004_deb_repo_republish_candidates.txt was not readable.
You can manually use an alternate input file by running "foreman-rake katello:upgrades:3.13:republish_deb_metadata[<path>]"
=============================================
Upgrade Step 12/15: katello:upgrades:3.15:set_sub_facet_dmi_uuid. =============================================
Upgrade Step 13/15: katello:upgrades:3.15:reindex_rpm_modular. =============================================
Upgrade Step 14/15: katello:upgrades:3.16:update_applicable_el8_hosts. =============================================
Upgrade Step 15/15: katello:upgrades:3.18:add_cvv_export_history_metadata.   Success!
  * Foreman is running at https://sat6.example.com
      Initial credentials are admin / sBHLrUi3cF8ucoa9
  * To install an additional Foreman proxy on separate machine continue by running:

      foreman-proxy-certs-generate --foreman-proxy-fqdn "$FOREMAN_PROXY" --certs-tar "/root/$FOREMAN_PROXY-certs.tar"
  * Foreman Proxy is running at https://sat6.example.com:9090

  The full log is at /var/log/foreman-installer/katello.log
2022-05-11 15:25:02 [NOTICE] [post] All hooks in group post finished
[root@sat6 ~]#


<h1> hammer Commands </h1>
[root@sat6 ~]# hammer subscription list --organization "msa"
---|------|------|------|----------|---------|---------|------------|----------|----------|---------
ID | UUID | NAME | TYPE | CONTRACT | ACCOUNT | SUPPORT | START DATE | END DATE | QUANTITY | CONSUMED
---|------|------|------|----------|---------|---------|------------|----------|----------|---------
[root@sat6 ~]#

root@sat6 ~]# hammer subscription list --organization "msa"
---|------|------|------|----------|---------|---------|------------|----------|----------|---------
ID | UUID | NAME | TYPE | CONTRACT | ACCOUNT | SUPPORT | START DATE | END DATE | QUANTITY | CONSUMED
---|------|------|------|----------|---------|---------|------------|----------|----------|---------
[root@sat6 ~]# hammer product create \
> --name "el7_repos" \
> --description "Various repositories to use with CentOS 7" --organization "msa"
Product created.
[root@sat6 ~]# hammer product list --organization "msa"
---|-----------|-------------------------------------------|--------------|--------------|-----------
ID | NAME      | DESCRIPTION                               | ORGANIZATION | REPOSITORIES | SYNC STATE
---|-----------|-------------------------------------------|--------------|--------------|-----------
1  | el7_repos | Various repositories to use with CentOS 7 | msa         | 0            |
---|-----------|-------------------------------------------|--------------|--------------|-----------
[root@sat6 ~]#

[root@sat6 ~]# hammer product list --organization "msa"
---|-----------|-------------------------------------------|--------------|--------------|-----------
ID | NAME      | DESCRIPTION                               | ORGANIZATION | REPOSITORIES | SYNC STATE
---|-----------|-------------------------------------------|--------------|--------------|-----------
1  | el7_repos | Various repositories to use with CentOS 7 | msa         | 0            |
---|-----------|-------------------------------------------|--------------|--------------|-----------
[root@sat6 ~]#

[root@sat6 ~]# mkdir /etc/pki/rpm-gpg/import/
[root@sat6 ~]#  cd /etc/pki/rpm-gpg/import/
[root@sat6 import]# wget http://mirror.centos.org/centos/7/os/x86_64/RPM-GPG-KEY-CentOS-7
--2022-05-12 16:06:25--  http://mirror.centos.org/centos/7/os/x86_64/RPM-GPG-KEY-CentOS-7
Resolving mirror.centos.org (mirror.centos.org)... 67.220.193.10, 2607:f2d8:1:e::10
Connecting to mirror.centos.org (mirror.centos.org)|67.220.193.10|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1690 (1.7K)
Saving to: â€˜RPM-GPG-KEY-CentOS-7â€™

100%[==================================================================================================================>] 1,690       --.-K/s   in 0.001s

2022-05-12 16:06:25 (3.02 MB/s) - â€˜RPM-GPG-KEY-CentOS-7â€™ saved [1690/1690]

[root@sat6 import]#

[root@sat6 import]# hammer gpg create \
> --key "RPM-GPG-KEY-CentOS-7" \
> --name "RPM-GPG-KEY-CentOS-7" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]#

[root@sat6 import]# hammer gpg create \
> --key "RPM-GPG-KEY-EPEL-7Server" \
> --name "RPM-GPG-KEY-EPEL-7Server" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.


he gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]# wget https://repo.mysql.com/RPM-GPG-KEY-mysqlwget https://repo.mysql.com/RPM-GPG-KEY-mysqlwget https://repo.mysql.com/RPM-GPG-KEY-mysql
--2022-05-12 16:11:17--  https://repo.mysql.com/RPM-GPG-KEY-mysqlwget
Resolving repo.mysql.com (repo.mysql.com)... 104.126.40.229
Connecting to repo.mysql.com (repo.mysql.com)|104.126.40.229|:443... connected.
HTTP request sent, awaiting response... 404 Not Found
2022-05-12 16:11:18 ERROR 404: Not Found.

--2022-05-12 16:11:18--  https://repo.mysql.com/RPM-GPG-KEY-mysqlwget
Reusing existing connection to repo.mysql.com:443.
HTTP request sent, awaiting response... 404 Not Found
2022-05-12 16:11:18 ERROR 404: Not Found.

--2022-05-12 16:11:18--  https://repo.mysql.com/RPM-GPG-KEY-mysql
Reusing existing connection to repo.mysql.com:443.
HTTP request sent, awaiting response... 200 OK
Length: 1944 (1.9K) [text/plain]
Saving to: â€˜RPM-GPG-KEY-mysqlâ€™

100%[==================================================================================================================>] 1,944       --.-K/s   in 0s

2022-05-12 16:11:18 (406 MB/s) - â€˜RPM-GPG-KEY-mysqlâ€™ saved [1944/1944]

FINISHED --2022-05-12 16:11:18--
Total wall clock time: 0.7s
Downloaded: 1 files, 1.9K in 0s (406 MB/s)
[root@sat6 import]# hammer gpg create \
> --key "RPM-GPG-KEY-mysql" \
> --name "RPM-GPG-KEY-mysql" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]#


[root@sat6 import]# wget http://repo.zabbix.com/RPM-GPG-KEY-ZABBIX
--2022-05-12 16:13:08--  http://repo.zabbix.com/RPM-GPG-KEY-ZABBIX
Resolving repo.zabbix.com (repo.zabbix.com)... 178.128.6.101, 2604:a880:2:d0::2062:d001
Connecting to repo.zabbix.com (repo.zabbix.com)|178.128.6.101|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1333 (1.3K) [application/octet-stream]
Saving to: â€˜RPM-GPG-KEY-ZABBIXâ€™

100%[==================================================================================================================>] 1,333       --.-K/s   in 0s

2022-05-12 16:13:08 (68.4 MB/s) - â€˜RPM-GPG-KEY-ZABBIXâ€™ saved [1333/1333]

[root@sat6 import]# hammer gpg create \
> --key "RPM-GPG-KEY-ZABBIX" \
> --name "RPM-GPG-KEY-ZABBIX" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]#

[root@sat6 import]#  wget https://rpms.remirepo.net/RPM-GPG-KEY-remi
--2022-05-12 16:14:31--  https://rpms.remirepo.net/RPM-GPG-KEY-remi
Resolving rpms.remirepo.net (rpms.remirepo.net)... 109.238.14.107, 2a00:c70:1:109:238:14:107:1
Connecting to rpms.remirepo.net (rpms.remirepo.net)|109.238.14.107|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1340 (1.3K)
Saving to: â€˜RPM-GPG-KEY-remiâ€™

100%[==================================================================================================================>] 1,340       --.-K/s   in 0s

2022-05-12 16:14:32 (52.3 MB/s) - â€˜RPM-GPG-KEY-remiâ€™ saved [1340/1340]

[root@sat6 import]# hammer gpg create \
> --key "RPM-GPG-KEY-remi" \
> --name "RPM-GPG-KEY-remi" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]#

root@sat6 import]# wget https://artifacts.elastic.co/GPG-KEY-elasticsearch
--2022-05-12 16:15:54--  https://artifacts.elastic.co/GPG-KEY-elasticsearch
Resolving artifacts.elastic.co (artifacts.elastic.co)... 34.120.127.130, 2600:1901:0:1d7::
Connecting to artifacts.elastic.co (artifacts.elastic.co)|34.120.127.130|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1768 (1.7K) [application/pgp-keys]
Saving to: â€˜GPG-KEY-elasticsearchâ€™

100%[==================================================================================================================>] 1,768       --.-K/s   in 0.001s

2022-05-12 16:15:54 (2.33 MB/s) - â€˜GPG-KEY-elasticsearchâ€™ saved [1768/1768]

[root@sat6 import]# hammer gpg create \
> --key "GPG-KEY-elasticsearch" \
> --name "GPG-KEY-elasticsearch" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]#


The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
[root@sat6 import]# hammer gpg list  --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
---|-------------------------
ID | NAME
---|-------------------------
6  | GPG-KEY-elasticsearch
1  | RPM-GPG-KEY-CentOS-7
2  | RPM-GPG-KEY-EPEL-7Server
3  | RPM-GPG-KEY-mysql
5  | RPM-GPG-KEY-remi
4  | RPM-GPG-KEY-ZABBIX
---|-------------------------
[root@sat6 import]#


[root@sat6 ~]# cat el7-repo.sh
hammer repository create \
  --product "el7_repos" \
  --name "base_x86_64" \
  --label "base_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-7" \
  --url "http://mirror.centos.org/centos/7/os/x86_64/" \
  --organization "msa"
[root@sat6 ~]# bash el7-repo.sh
Repository created.
[root@sat6 ~]#

[root@sat6 ~]# vim el7-extra.sh
[root@sat6 ~]# bash el7-extra.sh
Repository created.
[root@sat6 ~]# cat el7-extra.sh
 hammer repository create \
  --product "el7_repos" \
  --name "extras_x86_64" \
  --label "extras_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-7" \
  --url "http://mirror.centos.org/centos/7/extras/x86_64/" \
  --organization "msa"
[root@sat6 ~]#


root@sat6 ~]# cat el7-update.sh
hammer repository create \
  --product "el7_repos" \
  --name "updates_x86_64" \
  --label "updates_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-7" \
  --url "http://mirror.centos.org/centos/7/updates/x86_64/" \
  --mirror-on-sync "no" \
  --organization "msa"

[root@sat6 ~]# bash el7-update.sh
Repository created.
[root@sat6 ~]#

[root@sat6 ~]# cat epel.sh
hammer repository create \
  --product "el7_repos" \
  --name "epel_x86_64" \
  --label "epel_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-EPEL-7Server" \
  --url "https://dl.fedoraproject.org/pub/epel/7Server/x86_64/" \
  --organization "msa"

[root@sat6 ~]# bash epel.sh
Repository created.
[root@sat6 ~]#

[root@sat6 ~]# cat msql.sh
hammer repository create \
  --product "el7_repos" \
  --name "mysql_57_x86_64" \
  --label "mysql_57_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-mysql" \
  --url "https://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/" \
  --organization "msa"
[root@sat6 ~]# bash msql.sh
Repository created.
[root@sat6 ~]#

[root@sat6 ~]# cat remi.sh
hammer repository create \
  --product "el7_repos" \
  --name "remi_php_72_x86_64" \
  --label "remi_php_72_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-remi" \
  --url "https://mirrors.ukfast.co.uk/sites/remi/enterprise/7/php72/x86_64/" \
  --organization "msa"

[root@sat6 ~]# bash remi.sh
Repository created.

[root@sat6 ~]# cat zabbix.sh
 hammer repository create \
  --product "el7_repos" \
  --name "zabbix_30_x86_64" \
  --label "zabbix_30_x86_64" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-ZABBIX" \
  --url "http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/" \
  --organization "msa"

[root@sat6 ~]# bash zabbix.sh
Repository created.

root@sat6 ~]# hammer repository list --organization "msa"
---|--------------------|-----------|--------------|-------------------------------------------------------------------
ID | NAME               | PRODUCT   | CONTENT TYPE | URL
---|--------------------|-----------|--------------|-------------------------------------------------------------------
1  | base_x86_64        | el7_repos | yum          | http://mirror.centos.org/centos/7/os/x86_64/
4  | epel_x86_64        | el7_repos | yum          | https://dl.fedoraproject.org/pub/epel/7Server/x86_64/
2  | extras_x86_64      | el7_repos | yum          | http://mirror.centos.org/centos/7/extras/x86_64/
5  | mysql_57_x86_64    | el7_repos | yum          | https://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/
6  | remi_php_72_x86_64 | el7_repos | yum          | https://mirrors.ukfast.co.uk/sites/remi/enterprise/7/php72/x86_64/
3  | updates_x86_64     | el7_repos | yum          | http://mirror.centos.org/centos/7/updates/x86_64/
7  | zabbix_30_x86_64   | el7_repos | yum          | http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/
---|--------------------|-----------|--------------|-------------------------------------------------------------------
[root@sat6 ~]#


hammer content-view create \
  --name "el7_content" \
  --description "Content view for CentOS 7" \
  --organization "msa"

[root@sat6 ~]# bash content_view.sh
Content view created.


[root@sat6 ~]# hammer product list --organization "msa"
---|-----------|-------------------------------------------|--------------|--------------|------------------
ID | NAME      | DESCRIPTION                               | ORGANIZATION | REPOSITORIES | SYNC STATE
---|-----------|-------------------------------------------|--------------|--------------|------------------
1  | el7_repos | Various repositories to use with CentOS 7 | msa         | 7            | Syncing Complete.
---|-----------|-------------------------------------------|--------------|--------------|------------------
[root@sat6 ~]#

[root@sat6 ~]# vim add-content-view.sh
[root@sat6 ~]# bash add-content-view.sh
The repository has been associated.
The repository has been associated.
The repository has been associated.
The repository has been associated.
The repository has been associated.
The repository has been associated.
The repository has been associated.
 .
[root@sat6 ~]# cat add-content-view.sh
for i in $(seq 1 16); do \
  hammer content-view add-repository \
  --name "el7_content" \
  --product "el7_repos" \
  --organization "msa" \
  --repository-id "$i"; \
  done

root@sat6 ~]# vim lifecycle_view.sh
[root@sat6 ~]# bash lifecycle_view.sh
Environment created.
[root@sat6 ~]# cat lifecycle_view.sh
hammer lifecycle-environment create \
  --name "stable" \
  --label "stable" \
  --prior "Library" \
  --organization "msa"


[root@sat6 ~]# hammer lifecycle-environment list --organization "msa"
---|---------|--------
ID | NAME    | PRIOR
---|---------|--------
3  | Library |
4  | stable  | Library
---|---------|--------
[root@sat6 ~]#

root@sat6 ~]# cat pusblish_content_view.sh
hammer content-view publish \
  --name "el7_content" \
  --description "Publishing repositories" \
  --organization "msa"

[root@sat6 ~]# bash pusblish_content_view.sh
[.....................................................................................................................................................................] [100%]
[root@sat6 ~]#

[root@sat6 ~]# bash pusblish_content_view.sh
[.....................................................................................................................................................................] [100%]
[root@sat6 ~]# hammer content-view version list --organization "msa"
---|-------------------------------|---------|-------------------------|-----------------------
ID | NAME                          | VERSION | DESCRIPTION             | LIFECYCLE ENVIRONMENTS
---|-------------------------------|---------|-------------------------|-----------------------
4  | el7_content 1.0               | 1.0     | Publishing repositories | Library
3  | Default Organization View 1.0 | 1.0     |                         | Library
---|-------------------------------|---------|-------------------------|-----------------------
[root@sat6 ~]#

[root@sat6 ~]# vim promote-lifeCycle.sh
[root@sat6 ~]# bash promote-lifeCycle.sh
[.....................................................................................................................................................................] [100%]
[root@sat6 ~]# cat promote-lifeCycle.sh
hammer content-view version promote \
  --content-view "el7_content" \
  --version "1.0" \
  --to-lifecycle-environment "stable" \
  --organization "msa"
[root@sat6 ~]#

[root@sat6 ~]# hammer content-view version list --organization "msa"
---|-------------------------------|---------|-------------------------|-----------------------
ID | NAME                          | VERSION | DESCRIPTION             | LIFECYCLE ENVIRONMENTS
---|-------------------------------|---------|-------------------------|-----------------------
4  | el7_content 1.0               | 1.0     | Publishing repositories | Library, stable
3  | Default Organization View 1.0 | 1.0     |                         | Library
---|-------------------------------|---------|-------------------------|-----------------------
[root@sat6 ~]#


[root@sat6 ~]# cat activationKey.sh
hammer activation-key create \
  --name "el7-key" \
  --description "Key to use with CentOS7" \
  --lifecycle-environment "stable" \
  --content-view "el7_content" \
  --unlimited-hosts \
  --organization "msa"

[root@sat6 ~]# bash activationKey.sh
Activation key created.
[root@sat6 ~]#

[root@sat6 ~]# hammer activation-key list --organization "msa"
---|---------|----------------|-----------------------|-------------
ID | NAME    | HOST LIMIT     | LIFECYCLE ENVIRONMENT | CONTENT VIEW
---|---------|----------------|-----------------------|-------------
1  | el7-key | 0 of Unlimited | stable                | el7_content
---|---------|----------------|-----------------------|-------------
[root@sat6 ~]#


[root@sat6 ~]# hammer subscription list --organization "msa"
---|----------------------------------|-----------|----------|----------|---------|---------|---------------------|---------------------|-----------|---------
ID | UUID                             | NAME      | TYPE     | CONTRACT | ACCOUNT | SUPPORT | START DATE          | END DATE            | QUANTITY  | CONSUMED
---|----------------------------------|-----------|----------|----------|---------|---------|---------------------|---------------------|-----------|---------
1  | 402880c580b54e8c0180ba802d52001e | el7_repos | Physical |          |         |         | 2022/05/12 23:00:03 | 2049/12/01 00:00:00 | Unlimited | 0
---|----------------------------------|-----------|----------|----------|---------|---------|---------------------|---------------------|-----------|---------
[root@sat6 ~]#

root@sat6 ~]# bash addActivationKey.sh
Subscription added to activation key.
[root@sat6 ~]# cat addActivationKey.sh
hammer activation-key add-subscription \
  --name "el7-key" \
  --quantity "1" \
  --subscription-id "1" \
  --organization "msa"

***

[root@sat6 ~]# hammer product create \
> --name "el8_repos" \
> --description "Repositories to use with CentOS 8 Linux" \
> --organization "msa"
Product created.
[root@sat6 ~]# hammer product list --organization "msa"
---|-----------|-------------------------------------------|--------------|--------------|------------------
ID | NAME      | DESCRIPTION                               | ORGANIZATION | REPOSITORIES | SYNC STATE
---|-----------|-------------------------------------------|--------------|--------------|------------------
1  | el7_repos | Various repositories to use with CentOS 7 | msa         | 7            | Syncing Complete.
2  | el8_repos | Repositories to use with CentOS 8 Linux   | msa         | 0            |
---|-----------|-------------------------------------------|--------------|--------------|------------------
[root@sat6 ~]#


[root@sat6 import]# wget https://www.centos.org/keys/RPM-GPG-KEY-CentOS-Official
--2022-05-12 23:17:45--  https://www.centos.org/keys/RPM-GPG-KEY-CentOS-Official
Resolving www.centos.org (www.centos.org)... 81.171.33.201, 35.178.203.231, 81.171.33.202, ...
Connecting to www.centos.org (www.centos.org)|81.171.33.201|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1683 (1.6K)
Saving to: ‘RPM-GPG-KEY-CentOS-Official’

100%[====================================================================================================================================>] 1,683       --.-K/s   in 0s

2022-05-12 23:17:47 (3.48 MB/s) - ‘RPM-GPG-KEY-CentOS-Official’ saved [1683/1683]

[root@sat6 import]#

[root@sat6 import]# cp /root/gpg-key-el8.sh .
[root@sat6 import]# bash gpg-key-el8.sh
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]# cat gpg-key-el8.sh
hammer gpg create \
 --key "RPM-GPG-KEY-CentOS-Official" \
  --name "RPM-GPG-KEY-CentOS-8" --organization "msa"
[root@sat6 import]#

[root@sat6 import]# vim /root/.hammer/cli.modules.d/foreman.yml
[root@sat6 import]# bash repo-centos8.sh
Repository created.
[root@sat6 import]# cat repo-centos8.sh
hammer repository create \
  --product "el8_repos" \
  --name "CentOS 8 Base RPMS" \
  --label "CentOS_8_Base_RPMS" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-8" \
  --url "http://centos.mirror.liquidtelecom.com/8/BaseOS/x86_64/os/" \
  --mirror-on-sync "no" \
  --organization "msa"
[root@sat6 import]#

[root@sat6 import]# bash centos8_AppsStream.sh
Repository created.
[root@sat6 import]# cat centos8_AppsStream.sh
hammer repository create \
  --product "el8_repos" \
  --name "CentOS 8 AppStream RPMS" \
  --label "CentOS_8_AppStream_RPMS" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-8" \
  --url "http://centos.mirror.liquidtelecom.com/8/AppStream/x86_64/os/" \
  --mirror-on-sync "no" \
  --organization "msa"
[root@sat6 import]#


root@sat6 import]# hammer repository list --organization "msa"
---|-------------------------|-----------|--------------|-------------------------------------------------------------------
ID | NAME                    | PRODUCT   | CONTENT TYPE | URL
---|-------------------------|-----------|--------------|-------------------------------------------------------------------
1  | base_x86_64             | el7_repos | yum          | http://mirror.centos.org/centos/7/os/x86_64/
30 | CentOS 8 AppStream RPMS | el8_repos | yum          | http://centos.mirror.liquidtelecom.com/8/AppStream/x86_64/os/
29 | CentOS 8 Base RPMS      | el8_repos | yum          | http://centos.mirror.liquidtelecom.com/8/BaseOS/x86_64/os/
4  | epel_x86_64             | el7_repos | yum          | https://dl.fedoraproject.org/pub/epel/7Server/x86_64/
2  | extras_x86_64           | el7_repos | yum          | http://mirror.centos.org/centos/7/extras/x86_64/
5  | mysql_57_x86_64         | el7_repos | yum          | https://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/
6  | remi_php_72_x86_64      | el7_repos | yum          | https://mirrors.ukfast.co.uk/sites/remi/enterprise/7/php72/x86_64/
3  | updates_x86_64          | el7_repos | yum          | http://mirror.centos.org/centos/7/updates/x86_64/
7  | zabbix_30_x86_64        | el7_repos | yum          | http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/
---|-------------------------|-----------|--------------|-------------------------------------------------------------------
[root@sat6 import]#

 
hammer repository create \
  --product "el8_repos" \
  --name "CentOS 8 Base RPMS" \
  --label "CentOS_8_Base_RPMS" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-8" \
  --url "http://centos.mirror.liquidtelecom.com/8/BaseOS/x86_64/os/" \
  --mirror-on-sync "no" \
  --organization "msa"
  
  
  
 
  
  hammer repository create \
  --product "el8_repos" \
  --name "CentOS 8 AppStream RPMS" \
  --label "CentOS_8_AppStream_RPMS" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-8" \
  --url "http://centos.mirror.liquidtelecom.com/8/AppStream/x86_64/os/" \
  --mirror-on-sync "no" \
  --organization "msa"
  
   
  http://linuxsoft.cern.ch/centos-vault/6.10/os/x86_64/RPM-GPG-KEY-CentOS-6 
  
  cat repo-centos8.sh
  hammer repository create \
  --product "el6_repos" \
  --name "CentOS 6" \
  --label "CentOS_6" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-6" \
  -- url "http://linuxsoft.cern.ch/centos-vault/6.10/os/" \
  --mirror-on-sync "no" \
  --organization "msa"
  
  
  [root@sat6 ~]# bash create_prod6.sh
Product created.
[root@sat6 ~]# hammer product list --organization "msa"
---|-----------|-------------------------------------------|--------------|--------------|--------------                                         ----
ID | NAME      | DESCRIPTION                               | ORGANIZATION | REPOSITORIES | SYNC STATE                                            
---|-----------|-------------------------------------------|--------------|--------------|--------------                                         ----
3  | el6_repos | Repositories to use with CentOS 6 Linux   | msa         | 0            |                                                       
1  | el7_repos | Various repositories to use with CentOS 7 | msa         | 7            | Syncing Compl                                         ete.
2  | el8_repos | Repositories to use with CentOS 8 Linux   | msa         | 2            |                                                       
---|-----------|-------------------------------------------|--------------|--------------|--------------                                         ----
[root@sat6 ~]# hammer product list --organization "msa"
---|-----------|-------------------------------------------|--------------|--------------|------------------
ID | NAME      | DESCRIPTION                               | ORGANIZATION | REPOSITORIES | SYNC STATE
---|-----------|-------------------------------------------|--------------|--------------|------------------
3  | el6_repos | Repositories to use with CentOS 6 Linux   | msa         | 0            |
1  | el7_repos | Various repositories to use with CentOS 7 | msa         | 7            | Syncing Complete.
2  | el8_repos | Repositories to use with CentOS 8 Linux   | msa         | 2            |
---|-----------|-------------------------------------------|--------------|--------------|------------------
[root@sat6 ~]# cat create_prod6.sh
hammer product create \
 --name "el6_repos" \
 --description "Repositories to use with CentOS 6 Linux" \
 --organization "msa"
[root@sat6 ~]#

hammer gpg create \
 --key "RPM-GPG-KEY-CentOS-6" \
  --name "RPM-GPG-KEY-CentOS-6" --organization "msa"

[root@sat6 import]# hammer gpg create \
> --key "RPM-GPG-KEY-CentOS-6" \
> --name "RPM-GPG-KEY-CentOS-6" --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
GPG Key created.
[root@sat6 import]# hammer gpg list  --organization "msa"
The gpg sub-command is deprecated and will be removed in one of the future versions. Please use the content-credentials command instead.
---|-------------------------
ID | NAME
---|-------------------------
6  | GPG-KEY-elasticsearch
8  | RPM-GPG-KEY-CentOS-6
1  | RPM-GPG-KEY-CentOS-7
7  | RPM-GPG-KEY-CentOS-8
2  | RPM-GPG-KEY-EPEL-7Server
3  | RPM-GPG-KEY-mysql
5  | RPM-GPG-KEY-remi
4  | RPM-GPG-KEY-ZABBIX
---|-------------------------
[root@sat6 import]#

[root@sat6 import]# bash repo-rhel6.sh
Repository created.
[root@sat6 import]# cat repo-rhel6.sh
hammer repository create \
  --product "el6_repos" \
  --name "CentOS 6" \
  --label "CentOS_6" \
  --content-type "yum" \
  --download-policy "on_demand" \
  --gpg-key "RPM-GPG-KEY-CentOS-6" \
  --url "http://linuxsoft.cern.ch/centos-vault/6.10/os/" \
  --mirror-on-sync "no" \
  --organization "msa"
[root@sat6 import]#


<b>Register Clinet</b> 

[root@srv1 ~]# ssh-copy-id -i /root/.ssh/id_rsa.pub sat6
The authenticity of host 'sat6 (192.168.0.69)' can't be established.
ECDSA key fingerprint is b7:af:26:df:90:6b:0b:81:d0:60:ca:4f:ec:ad:20:3c.
Are you sure you want to continue connecting (yes/no)? yes
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@sat6's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'sat6'"
and check to make sure that only the key(s) you wanted were added.

[root@srv1 ~]# yum install subscription-manager -y
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: muug.ca
 * extras: muug.ca
 * updates: muug.ca
Resolving Dependencies
--> Running transaction check
---> Package subscription-manager.x86_64 0:1.24.50-1.el7.centos will be installed
--> Processing Dependency: subscription-manager-rhsm = 1.24.50 for package: subscription-manager-1.24.50-1.el7.centos.x86_64
--> Processing Dependency: python-dmidecode >= 3.12.2-2 for package: subscription-manager-1.24.50-1.el7.centos.x86_64
--> Processing Dependency: python-syspurpose for package: subscription-manager-1.24.50-1.el7.centos.x86_64
--> Processing Dependency: python-setuptools for package: subscription-manager-1.24.50-1.el7.centos.x86_64
--> Processing Dependency: python-inotify for package: subscription-manager-1.24.50-1.el7.centos.x86_64
-python-dmidecode-3.10.13-11.el7.x86_64                                                                                                                                                              13/13

Installed:
  subscription-manager.x86_64 0:1.24.50-1.el7.centos

Dependency Installed:
  python-backports.x86_64 0:1.0-8.el7                      python-backports-ssl_match_hostname.noarch 0:3.5.0.1-1.el7            python-dateutil.noarch 0:1.5-7.el7      python-ethtool.x86_64 0:0.8-8.el7
  python-inotify.noarch 0:0.9.4-4.el7                      python-ipaddress.noarch 0:1.0.16-2.el7                                python-setuptools.noarch 0:0.9.8-7.el7  python-syspurpose.x86_64 0:1.24.50-1.el7.centos
  subscription-manager-rhsm.x86_64 0:1.24.50-1.el7.centos  subscription-manager-rhsm-certificates.x86_64 0:1.24.50-1.el7.centos

Dependency Updated:
  python-dmidecode.x86_64 0:3.12.2-4.el7

Complete!
[root@srv1 ~]# curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://sat6/pub/katello-ca-consumer-latest.noarch.rpm
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  8540  100  8540    0     0  27728      0 --:--:-- --:--:-- --:--:-- 27817
[root@srv1 ~]# ls ltr
ls: cannot access ltr: No such file or directory
[root@srv1 ~]# ls -ltr
total 16
-rw-------. 1 root root 1585 Feb 24 14:15 anaconda-ks.cfg
-rw-r--r--  1 root root 8540 May 15 11:36 katello-ca-consumer-latest.noarch.rpm
[root@srv1 ~]# yum localinstall katello-ca-consumer-latest.noarch.rpm -y
Loaded plugins: fastestmirror, langpacks, product-id, search-disabled-repos, subscription-manager

This system is not registered with an entitlement server. You can use subscription-manager to register.

Examining katello-ca-consumer-latest.noarch.rpm: katello-ca-consumer-sat6.example.com-1.0-1.noarch
Marking katello-ca-consumer-latest.noarch.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package katello-ca-consumer-sat6.example.com.noarch 0:1.0-1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================================
 Package                                                             Arch                                  Version                               Repository                                                         Size
=========================================================================================================================================================================================================================
Installing:
 katello-ca-consumer-sat6.example.com                                noarch                                1.0-1                                 /katello-ca-consumer-latest.noarch                                 20 k

Transaction Summary
=========================================================================================================================================================================================================================
Install  1 Package

Total size: 20 k
Installed size: 20 k
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : katello-ca-consumer-sat6.example.com-1.0-1.noarch                                                                                                                                                     1/1
  Verifying  : katello-ca-consumer-sat6.example.com-1.0-1.noarch                                                                                                                                                     1/1

Installed:
  katello-ca-consumer-sat6.example.com.noarch 0:1.0-1

Complete!
[root@srv1 ~]# ls -ltr /etc/rhsm/ca/katello-*
-rw-r--r-- 1 root root 8102 May 15 11:36 /etc/rhsm/ca/katello-server-ca.pem
-rw-r--r-- 1 root root 8102 May 15 11:36 /etc/rhsm/ca/katello-default-ca.pem
[root@srv1 ~]#


 el7-key
 
 # subscription-manager register --org="msa" --activationkey="el7-key"
 
 [root@srv1 ~]# [root@client ~]# yum -y install http://fedorapeople.org/groups/katello/releases/yum/3.2/client/el7/x86_64/katello-client-repos-latest.rpm
-bash: [root@client: command not found
[root@srv1 ~]# [root@client ~]# yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
[root@srv1 ~]# yum -y install http://fedorapeople.org/groups/katello/releases/yum/3.2/client/el7/x86_64/katello-client-repos-latest.rpm
Loaded plugins: fastestmirror, langpacks, product-id, search-disabled-repos, subscription-manager
katello-client-repos-latest.rpm                                                                                                                                                                   | 8.6 kB  00:00:00
Examining /var/tmp/yum-root-dLTkXS/katello-client-repos-latest.rpm: katello-client-repos-3.2.0-4.el7.noarch
Marking /var/tmp/yum-root-dLTkXS/katello-client-repos-latest.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package katello-client-repos.noarch 0:3.2.0-4.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================================
 Package                                                 Arch                                      Version                                         Repository                                                       Size
=========================================================================================================================================================================================================================
Installing:
 katello-client-repos                                    noarch                                    3.2.0-4.el7                                     /katello-client-repos-latest                                    1.4 k

Transaction Summary
=========================================================================================================================================================================================================================
Install  1 Package

Total size: 1.4 k
Installed size: 1.4 k
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : katello-client-repos-3.2.0-4.el7.noarch                                                                                                                                                               1/1
  Verifying  : katello-client-repos-3.2.0-4.el7.noarch                                                                                                                                                               1/1

Installed:
  katello-client-repos.noarch 0:3.2.0-4.el7

Complete!
[root@srv1 ~]# yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
Loaded plugins: fastestmirror, langpacks, product-id, search-disabled-repos, subscription-manager
epel-release-latest-7.noarch.rpm                                                                                                                                                                  |  15 kB  00:00:00
Examining /var/tmp/yum-root-dLTkXS/epel-release-latest-7.noarch.rpm: epel-release-7-14.noarch
Marking /var/tmp/yum-root-dLTkXS/epel-release-latest-7.noarch.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package epel-release.noarch 0:7-14 will be installed
--> Finished Dependency Resolution
katello-client/x86_64                                                                                                                                                                             | 3.6 kB  00:00:00
katello-client/x86_64/group_gz                                                                                                                                                                    |  414 B  00:00:00
katello-client/x86_64/primary_db                                                                                                                                                                  | 8.6 kB  00:00:00

Dependencies Resolved

=========================================================================================================================================================================================================================
 Package                                            Arch                                         Version                                       Repository                                                           Size
=========================================================================================================================================================================================================================
Installing:
 epel-release                                       noarch                                       7-14                                          /epel-release-latest-7.noarch                                        25 k

Transaction Summary
=========================================================================================================================================================================================================================
Install  1 Package

Total size: 25 k
Installed size: 25 k
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : epel-release-7-14.noarch                                                                                                                                                                              1/1
  Verifying  : epel-release-7-14.noarch                                                                                                                                                                              1/1

Installed:
  epel-release.noarch 0:7-14

Complete!
[root@srv1 ~]# systemctl start goferd
Failed to start goferd.service: Unit not found.
[root@srv1 ~]# systemctl restart goferd
Failed to restart goferd.service: Unit not found.
[root@srv1 ~]# goferd.service: Unit not found.
-bash: goferd.service:: command not found
[root@srv1 ~]# systemctl  status goferd
Unit goferd.service could not be found.
[root@srv1 ~]# systemctl  goferd status
Unknown operation 'goferd'.
[root@srv1 ~]# systemctl  status goferd.ervice
Unit goferd.ervice.service could not be found.
[root@srv1 ~]# yum install katello-agent
Loaded plugins: fastestmirror, langpacks, product-id, search-disabled-repos, subscription-manager
epel/x86_64/metalink                                                                                                                                                                              |  18 kB  00:00:00
https://muug.ca/mirror/fedora-epel/7/x86_64/repodata/repomd.xml: [Errno 14] curl#60 - "The certificate issuer's certificate has expired.  Check your system date and time."
Trying other mirror.
It was impossible to connect to the CentOS servers.
This could mean a connectivity issue in your environment, such as the requirement to configure a proxy,
or a transparent proxy that tampers with TLS security, or an incorrect system clock.
Please collect information about the specific failure that occurs in your environment,
using the instructions in: https://access.redhat.com/solutions/1527033 and create a bug on https://bugs.centos.org/

epel                                                                                                                                                                                              | 4.7 kB  00:00:00
(1/3): epel/x86_64/group_gz                                                                                                                                                                       |  96 kB  00:00:00
(2/3): epel/x86_64/updateinfo                                                                                                                                                                     | 1.0 MB  00:00:01
(3/3): epel/x86_64/primary_db                                                                                                                                                                     | 7.0 MB  00:00:02
Loading mirror speeds from cached hostfile
 * base: muug.ca
 * epel: mirrors.vcea.wsu.edu
 * extras: muug.ca
 * updates: muug.ca
Resolving Dependencies
--> Running transaction check
---> Package katello-agent.noarch 0:2.7.0-1.el7 will be installed
--> Processing Dependency: python-pulp-agent-lib >= 2.6 for package: katello-agent-2.7.0-1.el7.noarch
--> Processing Dependency: python-gofer-proton >= 2.5 for package: katello-agent-2.7.0-1.el7.noarch
--> Processing Dependency: pulp-rpm-handlers >= 2.6 for package: katello-agent-2.7.0-1.el7.noarch
--> Processing Dependency: gofer >= 2.5 for package: katello-agent-2.7.0-1.el7.noarch
--> Processing Dependency: katello-agent-fact-plugin for package: katello-agent-2.7.0-1.el7.noarch
--> Running transaction check
---> Package gofer.noarch 0:2.7.6-1.el7 will be installed
--> Processing Dependency: python-gofer = 2.7.6 for package: gofer-2.7.6-1.el7.noarch
---> Package katello-agent-fact-plugin.noarch 0:2.7.0-1.el7 will be installed
---> Package pulp-rpm-handlers.noarch 0:2.9.3-1.el7 will be installed
--> Processing Dependency: python-pulp-rpm-common = 2.9.3 for package: pulp-rpm-handlers-2.9.3-1.el7.noarch
---> Package python-gofer-proton.noarch 0:2.7.6-1.el7 will be installed
--> Processing Dependency: python-qpid-proton >= 0.9-5 for package: python-gofer-proton-2.7.6-1.el7.noarch
---> Package python-pulp-agent-lib.noarch 0:2.9.3-1.el7 will be installed
--> Processing Dependency: python-pulp-common = 2.9.3 for package: python-pulp-agent-lib-2.9.3-1.el7.noarch
--> Running transaction check
---> Package python-gofer.noarch 0:2.7.6-1.el7 will be installed
---> Package python-pulp-common.noarch 0:2.9.3-1.el7 will be installed
--> Processing Dependency: python-isodate >= 0.5.0-1.pulp for package: python-pulp-common-2.9.3-1.el7.noarch
---> Package python-pulp-rpm-common.noarch 0:2.9.3-1.el7 will be installed
---> Package python-qpid-proton.x86_64 0:0.14.0-2.el7 will be installed
--> Processing Dependency: qpid-proton-c(x86-64) = 0.14.0-2.el7 for package: python-qpid-proton-0.14.0-2.el7.x86_64
--> Processing Dependency: libqpid-proton.so.8()(64bit) for package: python-qpid-proton-0.14.0-2.el7.x86_64
--> Running transaction check
---> Package python-isodate.noarch 0:0.5.4-8.el7 will be installed
---> Package qpid-proton-c.x86_64 0:0.14.0-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================================
Install  1 Package (+11 Dependent packages)

Total download size: 1.0 M
Installed size: 3.2 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/katello-client/packages/katello-agent-2.7.0-1.el7.noarch.rpm: Header V3 RSA/SHA1 Signature, key ID bc62d13f: NOKEY                                    ]  0.0 B/s |    0 B  --:--:-- ETA
Proot@srv1 ~]#



</pre>
