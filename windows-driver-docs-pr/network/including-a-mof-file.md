---
title: 包含 MOF 文件
description: 包含 MOF 文件
ms.assetid: 87ef7156-d204-4797-b805-a50d9a4c509d
keywords:
- 自定义 Guid WDK 网络
- WMI WDK 网络、 Guid
- Oid WDK 网络 WMI
- Guid WDK 网络
- Windows Management Instrumentation WDK 网络 Guid
- MOF 文件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b9b6c610847fd0378f736b22eae4d6e3aa560b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374848"
---
# <a name="including-a-mof-file"></a>包含 MOF 文件





必须包括所有的自定义 Guid 映射到微型端口驱动程序的自定义 Oid 必须编译并包含在微型端口驱动程序的资源的托管的对象格式 (MOF) 文件中的说明 (\*.rc) 文件。

MOF 源文件必须是类型 MOFDATA 的而且必须具有的.mof 扩展。 必须将 MOF 源代码文件编译为二进制文件与[Mofcomp.exe](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file) ，并必须检查此文件，其[Wmimofck.exe](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)。

必须将以下行插入微型端口驱动程序的资源文件中 (\*.rc) 包括 MOF 二进制文件：

```Text
NdisMofResource MOFDATA filename.bmf
```

*文件名*表示 MOF 源文件的文件名。

 

 





