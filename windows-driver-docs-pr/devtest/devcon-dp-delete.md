---
title: DevCon Dp_delete
description: 从本地计算机上的驱动程序存储区中删除第三方 (OEM) 驱动程序包。 此命令将删除 INF 文件、PNF 文件和关联的目录文件 () 。
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
ms.openlocfilehash: 57d5ee6e5167bda9ace7a1c1ce292e3ab36f3833
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798345"
---
# <a name="devcon-dp_delete"></a>DevCon Dp \_ 删除

从本地计算机上的驱动程序存储区中删除第三方 (OEM) 驱动程序包。 此命令将删除 INF 文件、PNF 文件和关联的目录文件 () 。

```command
    devcon [-f] dp_delete inf
```

## <a name="parameters"></a>参数

**-f** 即使设备正在使用驱动程序包，此参数也会将其删除。

*inf* INF 文件的原始文件名 \* 。 将驱动程序包添加到驱动程序存储区（如使用 [**DevCon dp \_ add**](devcon-dp-add.md)）时，Windows 会将具有此格式的文件名分配给 INF 文件。

## <a name="comments"></a>注释

### <a name="sample-usage"></a>示例用法

```command
devcon dp_delete oem2.inf
devcon -f dp_delete oem0.inf
```
