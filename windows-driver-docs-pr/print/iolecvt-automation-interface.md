---
title: IOleCvt 自动化接口
description: IOleCvt 自动化接口
MS-HAID:
- webfnc\_0ca4054a-768a-44b9-bb7e-84a5cb81349b.xml
- print.iolecvt\_automation\_interface
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 286ab231-c215-45cc-b0da-97ec8adf2de1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01fba7e9303d79ef2962788508a46eaec4e3c6ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525485"
---
# <a name="iolecvt-automation-interface"></a>IOleCvt 自动化接口

自动化界面**IOleCvt**对象启用 ASP Web 页后，可以执行各种从一种格式的字符串转换到另一个。 这些地方包括：

-   从 Unicode 到 ANSI 的转换

-   从 ANSI 到 Unicode 的转换

-   从 Unicode 转换为 utf-8 （UCS 转换格式 8）

-   从 Unicode 使用为使用另一个代码页的 Unicode 代码页转换

尽管大多数应用程序现在使用 Unicode (utf-16) 编码为字符数据，但某些 Windows 桌面应用程序使用基于 Windows 代码页的字符集。 代码页将国际字符分配给大于 127 的 ANSI 字符代码。 有关代码页的详细信息，请参阅 Windows SDK 文档。

**IOleCvt** Windows 2000 及更高版本支持的接口。

编程标识符**IOleCvt**对象是 OlePrn.OleCvt。

有关如何对访问打印机从 ASP Web 页面的详细信息，请参阅[Internet 打印](https://docs.microsoft.com/windows-hardware/drivers/print/internet-printing)。

中的"属性 get"操作**IOleCvt**接口以下部分所述：

[IOleCvt 属性 Get 操作](iolecvt-property-get-operations.md)
