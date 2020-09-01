---
title: ISNMP 自动化接口
description: ISNMP 自动化接口
MS-HAID:
- webfnc\_4ff82461-8ece-4336-8f86-9461ad4ec8d7.xml
- print.isnmp\_automation\_interface
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 63f2f14d-ea9d-437c-9853-06889219627d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff46dd244fa9c50a64951401be69590cd4ab9249
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218197"
---
# <a name="isnmp-automation-interface"></a>ISNMP 自动化接口

**ISNMP**对象的自动化接口实质上是 (SNMP) 管理 API 的简单网络管理协议中的函数的 OLE 自动化包装。 通过 **ISNMP** 接口，ASP 网页可以设置和检索与 (oid) 的 SNMP 对象标识符相关联的值。 有关 SNMP 管理 API 的详细信息，请参阅 Windows SDK 文档。

**ISNMP**接口仅适用于使用 MICROSOFT 标准 TCIP/IP[端口监视器](./port-monitors.md)的打印机。 

**ISNMP**对象的编程标识符为 OlePrn. OleSNMP。

有关如何从 ASP 网页访问打印机的详细信息，请参阅 [Internet 打印](./internet-printing.md)。

以下部分介绍了 **ISNMP** 接口中的方法：

[ISNMP 方法](isnmp-methods.md)