---
title: 省略 LayoutFile 和 CatalogFile 信息
description: 省略 LayoutFile 和 CatalogFile 信息
keywords:
- INF 文件 WDK 显示，LayoutFile 指令
- INF 文件 WDK 显示，CatalogFile 指令
- CatalogFile 指令 WDK 显示
- LayoutFile 指令 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d4c8514fb95f1ecff1bc1ff51266d27f97e4dc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795005"
---
# <a name="omitting-layoutfile-and-catalogfile-information"></a>省略 LayoutFile 和 CatalogFile 信息


不得在 "**版本**" 部分中指定 **LayoutFile** 和 **CatalogFile** 指令的任何信息。 下面的示例演示一个典型 **版本** 部分：

```inf
[Version]
Signature="$Windows NT$"
Provider=%MSFT%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000
```

有关版本部分以及与 **版本****关联的指令** 的详细信息，请参阅 [**INF 版本部分**](../install/inf-version-section.md)。

 

