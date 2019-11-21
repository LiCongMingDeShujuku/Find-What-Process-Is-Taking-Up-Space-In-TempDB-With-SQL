![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 在TempDB中查找占用空间的程序SQL
#### Find What Process Is Taking Up Space In TempDB With SQL
**TIME STAMP**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这是我编写的一个脚本，可以找出哪些程序占用了TempDB中的空间，以及程序的来源。


## English
Here’s a script I threw together to find what process is taking up space in the TempDB, and where the process came from.

---
## Logic
```SQL
--find what objects are taking up the most TempDB space and where the process is coming from
--查找哪些对象占用了最多的TempDB空间以及程序的来源
use master;
set nocount on
select
    sddssu.session_id
,   'login name'        = sdes.login_name
,   'from device'       = sdes.host_name
,   'database'      = db_name(sddssu.database_id)
,   'space consumed in gb'  = (sddssu.user_objects_alloc_page_count *8 / 1024 / 2014)
,   'process'       = sder.command
,   'statement'     = sdest.text
from   
    sys.dm_db_session_space_usage sddssu 
    join sys.dm_exec_requests sder on sddssu.session_id = sder.session_id
    cross apply sys.dm_exec_sql_text(sder.sql_handle) sdest
    join sys.dm_exec_sessions sdes on sdes.session_id   = sder.session_id
where  
    db_name(sddssu.database_id) in ('tempdb')
    and sddssu.user_objects_alloc_page_count > 0


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

