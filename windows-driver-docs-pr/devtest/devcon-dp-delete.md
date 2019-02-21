---
title: DevCon Dp_delete
description: 从本地计算机上的驱动程序存储中删除第三方 (OEM) 驱动程序包。 此命令删除 INF 文件、 PNF 文件和关联的目录文件 (.cat)。
ms.assetid: bc9d8d66-4aa1-423b-b907-40a8c0194eb1
keywords:
- DevCon Dp_delete 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Dp_delete
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 582f8aac06c8de1f30f70575b49f9a4d55ebe368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540389"
---
# <a name="devcon-dpdelete"></a>DevCon Dp\_删除


从本地计算机上的驱动程序存储中删除第三方 (OEM) 驱动程序包。 此命令删除 INF 文件、 PNF 文件和关联的目录文件 (.cat)。

```
    devcon dp_delete [-f] inf
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
即使设备正在使用它时，此参数将删除驱动程序包。

<span id="_______inf______"></span><span id="_______INF______"></span> *inf*   
OEM\*.inf 文件名的 INF 文件。 Windows 将使用此格式的文件名称分配给 INF 文件时您将添加驱动程序包到驱动程序存储区，例如通过使用[ **DevCon dp\_添加**](devcon-dp-add.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon dp_delete oem2.inf
devcon dp_delete oem0.inf -f
```









