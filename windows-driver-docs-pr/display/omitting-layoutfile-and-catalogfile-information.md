---
title: 忽略 LayoutFile 和 CatalogFile 信息
description: 忽略 LayoutFile 和 CatalogFile 信息
ms.assetid: e34302b9-0fb4-462b-9fa6-5ae51e83cd8b
keywords:
- INF 文件 WDK 显示、 LayoutFile 指令
- INF 文件 WDK 显示、 CatalogFile 指令
- CatalogFile 指令 WDK 显示
- LayoutFile 指令 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e91cfb940c45135048c58fb346701b223b3051de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522524"
---
# <a name="omitting-layoutfile-and-catalogfile-information"></a>忽略 LayoutFile 和 CatalogFile 信息


您必须指定的任何信息**LayoutFile**并**CatalogFile**中的指令**版本**部分。 下面的示例演示一个典型**版本**部分：

```inf
[Version]
Signature="$Windows NT$"
Provider=%MSFT%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000
```

有关详细信息**版本**部分，并与之关联的指令**版本**，请参阅[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)。

 

 





