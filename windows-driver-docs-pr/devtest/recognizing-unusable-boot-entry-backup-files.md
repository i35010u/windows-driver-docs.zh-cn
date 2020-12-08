---
title: 识别不可用的启动项备份文件
description: 识别不可用的启动项备份文件
keywords:
- NVRAM 启动选项 WDK，
- EFI NVRAM 启动选项 WDK，
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1a7ea3baebf7f47e2452bfb4aaef0caae267bc5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839745"
---
# <a name="recognizing-unusable-boot-entry-backup-files"></a>识别不可用的启动项备份文件

遗憾的是，启动项备份副本并非始终可用。

在 EFI 环境中，应用程序和驱动程序通过分区 GUID 来识别磁盘分区。 如果磁盘分区 GUID 由于任何原因而发生更改，则启动项备份副本中的分区 GUID 将不再有效，且 EFI 启动加载程序将无法使用备份副本启动系统。

以下 Bootcfg 示例显示了使用无效分区 Guid 导入的启动条目。

```
Boot entry ID:    4
OS Friendly Name: Windows Server 2003 - mydebug
OsLoadOptions:    /debug /debugport=com1 /baudrate=115200
BootFilePath:     (null)
OsFilePath:       (null)
```

在这种情况下，你必须通过从操作系统安装中复制另一个启动项，然后更改参数来重新创建启动项。
