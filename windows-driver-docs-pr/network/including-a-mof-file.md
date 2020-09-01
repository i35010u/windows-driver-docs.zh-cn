---
title: 包含 MOF 文件
description: 包含 MOF 文件
ms.assetid: 87ef7156-d204-4797-b805-a50d9a4c509d
keywords:
- 自定义 Guid WDK 网络
- WMI WDK 网络，Guid
- Oid WDK 网络，WMI
- Guid WDK 网络
- Windows Management Instrumentation WDK 网络，Guid
- MOF 文件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 126e0dcfece6516e7392d034174c3efc2184a172
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217598"
---
# <a name="including-a-mof-file"></a>包含 MOF 文件





您必须包含所有自定义 Guid 的说明，这些 Guid 以托管对象格式映射到微型端口驱动程序的自定义 Oid (MOF) 文件必须编译并包含在微型端口驱动程序的资源 (\* .rc) 文件中。

MOF 源文件必须是 MOFDATA 类型，并且必须具有扩展名。 必须使用 [Mofcomp.exe](../kernel/compiling-a-driver-s-mof-file.md) 将 MOF 源文件编译为二进制文件，并且必须使用 [Wmimofck.exe](../kernel/using-wmimofck-exe.md)检查此文件。

必须在微型端口驱动程序的资源文件 (中插入以下行 \*) 才能包含 MOF 二进制文件：

```Text
NdisMofResource MOFDATA filename.bmf
```

*FileName* 表示 MOF 源文件的文件名。

 

