---
title: 打印网页的 ActiveX 对象
description: 打印网页的 ActiveX 对象
ms.assetid: 85c37895-542f-4399-bf87-517eaab99a09
keywords:
- 打印网页 WDK，ActiveX 对象
- 网页 WDK 打印机，ActiveX 对象
- 自定义打印网页 WDK，ActiveX 对象
- ActiveX 对象 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a624e6915d133ca9bae9dcbd91ec7a3971ea766
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343176"
---
# <a name="activex-objects-for-print-web-pages"></a>打印网页的 ActiveX 对象





三个 ActiveX 对象， [Iasphelp](https://msdn.microsoft.com/library/windows/hardware/ff550742)， [IOleCvt](https://msdn.microsoft.com/library/windows/hardware/ff551819)，并[ISNMP](https://msdn.microsoft.com/library/windows/hardware/ff554396)，提供有关打印的网页。 通过使用 VBScript 等脚本语言，ASP 文件可以通过自动化界面，访问每个对象。 Oleprn.dll 中实现的对象和接口。

以下列表包含每个接口的简短说明：

-   [Iasphelp 自动化接口](https://msdn.microsoft.com/library/windows/hardware/ff550742)使您可以获取与指定的打印机相关联的属性。

    此接口提供对信息不可用从 ASP 会话变量，并允许 ASP 页以获取有关对其调用页以外的打印机信息的访问。

-   [IOleCvt 自动化接口](https://msdn.microsoft.com/library/windows/hardware/ff551819)允许您将从 ANSI 字符串转换为 Unicode，并将字符串转换为 UTF8 格式，并将 Unicode 转换，反之亦然，字符串使用不同代码页。

-   [ISNMP 自动化接口](https://msdn.microsoft.com/library/windows/hardware/ff554396)允许您设置和检索与 SNMP Oid 关联的值，如果打印机支持 RFC 1759。

    [ISNMP](https://msdn.microsoft.com/library/windows/hardware/ff554396)接口可以仅用于使用 Microsoft 的 TCIP/IP 端口监视器的打印机。 此接口是实质上的 OLE 自动化包装器 SNMP 管理 API 函数。 有关这些函数的详细信息，请参阅 Microsoft Windows SDK 文档。

    对象可以使用数字字符串，指定 Id (Oid)，并将文本包含指定的 RFC 1759 名称字符串的管理信息基础 (MIB)。 其他 MIB 名称可以定义、 编译和安装自定义的 Mib，如果使用 Windows SDK 文档中所述。

有关 ActiveX 和自动化的信息，请参阅 Windows SDK 文档。

 

 




