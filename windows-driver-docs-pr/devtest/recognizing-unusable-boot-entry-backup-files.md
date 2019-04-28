---
title: 识别不可用的启动项备份文件
description: 识别不可用的启动项备份文件
ms.assetid: ff61c8e9-ad6b-4f3f-9c4b-72c24c27eda6
keywords:
- NVRAM 启动选项 WDK，
- EFI NVRAM 启动选项 WDK，
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e84f7deda6ff41901cbae59ef00ec3872886f77c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339747"
---
# <a name="recognizing-unusable-boot-entry-backup-files"></a>识别不可用的启动项备份文件

遗憾的是，启动项的备份副本并不总是可用。

在 EFI 环境中，应用程序和驱动程序确定磁盘分区由分区的 GUID。 如果出于任何原因发生更改磁盘分区 GUID，然后启动条目备份副本中的分区的 GUID 将不再有效，EFI 启动加载器无法使用备份副本来引导系统。

以下 Bootcfg 示例显示已导入具有无效的分区 Guid 的启动项。

```
Boot entry ID:    4
OS Friendly Name: Windows Server 2003 - mydebug
OsLoadOptions:    /debug /debugport=com1 /baudrate=115200
BootFilePath:     (null)
OsFilePath:       (null)
```

在这种情况下，必须重新启动项创建从操作系统安装中，复制另一个启动项，然后更改参数。
