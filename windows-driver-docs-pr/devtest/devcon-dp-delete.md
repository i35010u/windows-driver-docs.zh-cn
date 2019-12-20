---
title: DevCon Dp_delete
description: 从本地计算机上的驱动程序存储区中删除第三方（OEM）驱动程序包。 此命令删除 INF 文件、PNF 文件和关联的目录文件（.cat）。
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
ms.openlocfilehash: 3536a1a96fc305cfb7000dfda020d7beaab21255
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209483"
---
# <a name="devcon-dp_delete"></a>删除 DevCon Dp\_

从本地计算机上的驱动程序存储区中删除第三方（OEM）驱动程序包。 此命令删除 INF 文件、PNF 文件和关联的目录文件（.cat）。

```command
    devcon [-f] dp_delete inf
```

## <a name="parameters"></a>参数

**-f**即使设备正在使用驱动程序包，此参数也会将其删除。

*inf*INF 文件的 OEM\*.inf 文件名。 将驱动程序包添加到驱动程序存储区时，Windows 会将具有此格式的文件名分配给 INF 文件，例如通过使用[**DevCon dp\_add**](devcon-dp-add.md)。

## <a name="comments"></a>备注

### <a name="sample-usage"></a>示例用法

```command
devcon dp_delete oem2.inf
devcon -f dp_delete oem0.inf
```
