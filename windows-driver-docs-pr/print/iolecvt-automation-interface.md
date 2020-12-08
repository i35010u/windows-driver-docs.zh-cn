---
title: IOleCvt 自动化接口
description: IOleCvt 自动化接口
MS-HAID:
- webfnc\_0ca4054a-768a-44b9-bb7e-84a5cb81349b.xml
- print.iolecvt\_automation\_interface
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aba4617fca01ebd2bee047166dba8fc75a30d47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835611"
---
# <a name="iolecvt-automation-interface"></a>IOleCvt 自动化接口

通过 **IOleCvt** 对象的自动化接口，ASP 网页可执行各种格式的字符串转换。 其中包括：

-   从 Unicode 到 ANSI 的转换

-   从 ANSI 转换为 Unicode

-   从 Unicode 转换为 UTF-8 (UCS 转换格式 8) 

-   使用另一个代码页将一个代码页转换为 Unicode

尽管大多数应用程序现在使用 Unicode (字符数据的 UTF-16) 编码，但某些 Windows 桌面应用程序使用基于 Windows 代码页的字符集。 代码页将国际字符分配到大于127的 ANSI 字符代码。 有关代码页的详细信息，请参阅 Windows SDK 文档。

Windows 2000 及更高版本支持 **IOleCvt** 接口。

**IOleCvt** 对象的编程标识符为 OlePrn. OleCvt。

有关如何从 ASP 网页访问打印机的详细信息，请参阅 [Internet 打印](./internet-printing.md)。

以下部分介绍了 **IOleCvt** 接口中的 "属性 get" 操作：

[IOleCvt 属性获取操作](iolecvt-property-get-operations.md)
