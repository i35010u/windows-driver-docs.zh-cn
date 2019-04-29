---
title: Srcsrv.ini 文件
description: Srcsrv.ini 文件
ms.assetid: 5a3f5990-e43a-4c50-a16f-cbaa9f706ece
keywords:
- SrcSrv，Srcsrv.ini 文件
- Srcsrv.ini 文件
- SrcSrv, SRCSRV_INI_FILE environment variable
- SRCSRV_INI_FILE 环境变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c498cbf6e3856ed07dd9093ee997948303eaae8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365986"
---
# <a name="the-srcsrvini-file"></a>Srcsrv.ini 文件


Srcsrv.ini 文件是所有的源代码控制服务器的主列表。 每个条目具有以下格式：

```ini
MYSERVER=ServerInfo
```

当使用 Perforce *serverinfo 高速*包含到服务器，它使用的端口号后跟一个冒号后跟的完整网络路径。 例如：

```ini
MYSERVER=machine.corp.company.com:1666
```

Srcsrv.ini 是必需的文件时实际源索引生成使用与此包一起提供的模块。 此项创建一个别名，用于描述服务器信息。 值应是唯一的支持的每个服务器。

此外可以运行调试器的计算机上安装此文件。 SrcSrv 启动时，它会查找在 Srcsrv.ini 的值;这些值会重写.pdb 文件中包含的信息。 这样用户就可以配置调试器在调试时使用备用的源代码管理服务器。 但是，如果还管理您的服务器，并且不要重命名它们，应该有无需将此文件包含你的客户端调试器安装。

此文件还可在客户端上的其他用途。 有关详细信息，请参阅随 SrcSrv 工具一起安装的示例 Srcsrv.ini 文件。

### <a name="span-idusingadifferentlocationorfilenamespanspan-idusingadifferentlocationorfilenamespanusing-a-different-location-or-file-name"></a><span id="using_a_different_location_or_file_name"></span><span id="USING_A_DIFFERENT_LOCATION_OR_FILE_NAME"></span>使用不同的位置或文件名称

默认情况下，SrcSrv 使用其主配置文件作为名为 Srcsrv.ini，有关 Windows 调试工具安装目录的 srcsrv 子目录中的文件。

可以通过设置 SRCSRV 指定配置的不同文件\_INI\_文件环境变量等于所需的文件的完整路径和文件名称。

例如，如果多人想要共享单个配置文件，它们可以将其放在共享到所有其系统可访问，然后将如下所示的环境变量：

```console
set SRCSRV_INI_FILE=\\ourserver\ourshare\bestfile.txt
```

 

 





