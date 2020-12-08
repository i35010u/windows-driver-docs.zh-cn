---
title: Srcsrv.ini 文件
description: Srcsrv.ini 文件
keywords:
- Srcsrv.ini、Srcsrv.ini 文件
- Srcsrv.ini 文件
- Srcsrv.ini，SRCSRV_INI_FILE 环境变量
- SRCSRV_INI_FILE 环境变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66b8917d4f753730c2a01f8eaadc4d60fbcb404b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813899"
---
# <a name="the-srcsrvini-file"></a>Srcsrv.ini 文件


Srcsrv.ini 文件是所有源代码管理服务器的主列表。 每个条目均具有以下格式：

```ini
MYSERVER=ServerInfo
```

当使用 Perforce 时， *ServerInfo* 由服务器的完整网络路径组成，后跟一个冒号，后跟它使用的端口号。 例如：

```ini
MYSERVER=machine.corp.company.com:1666
```

当你实际使用此包附带的模块对生成进行源索引时，Srcsrv.ini 是必需的文件。 此项创建一个别名，用于描述服务器信息。 对于支持的每个服务器，值应是唯一的。

此文件也可以安装在运行调试器的计算机上。 当 Srcsrv.ini 启动时，它会查看值 Srcsrv.ini;这些值会替代 .pdb 文件中包含的信息。 这使用户能够将调试器配置为在调试时使用备用源代码管理服务器。 但是，如果您管理服务器并不重命名它们，则不需要在客户端调试器安装中包含此文件。

此文件还可以在客户端上提供其他目的。 有关详细信息，请参阅随 Srcsrv.ini tools 一起安装 Srcsrv.ini 文件示例。

### <a name="span-idusing_a_different_location_or_file_namespanspan-idusing_a_different_location_or_file_namespanusing-a-different-location-or-file-name"></a><span id="using_a_different_location_or_file_name"></span><span id="USING_A_DIFFERENT_LOCATION_OR_FILE_NAME"></span>使用其他位置或文件名

默认情况下，Srcsrv.ini 使用名为 Srcsrv.ini 的文件的主配置文件，该文件位于 Windows 调试工具的 srcsrv.ini 子目录下。

可以通过将 SRCSRV.INI \_ INI \_ 文件环境变量设置为所需文件的完整路径和文件名，为配置指定其他文件。

例如，如果多个用户需要共享一个配置文件，则可以将其放在所有系统都可以访问的共享上，然后设置如下所示的环境变量：

```console
set SRCSRV_INI_FILE=\\ourserver\ourshare\bestfile.txt
```

 

 





