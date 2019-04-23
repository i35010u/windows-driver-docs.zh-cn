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
ms.date: 04/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 240d2eed9fe8f4fe56f6236d586768c12cf90b08
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903505"
---
# <a name="devcon-dpdelete"></a>DevCon Dp\_删除

从本地计算机上的驱动程序存储中删除第三方 (OEM) 驱动程序包。 此命令删除 INF 文件、 PNF 文件和关联的目录文件 (.cat)。

```command
    devcon [-f] dp_delete inf
```

## <a name="parameters"></a>Parameters

**-f**即使设备正在使用它时，此参数将删除驱动程序包。

*inf* OEM\*.inf 文件名的 INF 文件。 Windows 将使用此格式的文件名称分配给 INF 文件时您将添加驱动程序包到驱动程序存储区，例如通过使用[ **DevCon dp\_添加**](devcon-dp-add.md)。

## <a name="comments"></a>备注

### <a name="sample-usage"></a>示例用法

```command
devcon dp_delete oem2.inf
devcon dp_delete oem0.inf -f
```
