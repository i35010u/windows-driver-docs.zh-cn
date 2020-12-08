---
title: 打印网页的 ActiveX 对象
description: 打印网页的 ActiveX 对象
keywords:
- 打印网页 WDK，ActiveX 对象
- 网页 WDK 打印机，ActiveX 对象
- 自定义的打印网页 WDK，ActiveX 对象
- ActiveX 对象 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d642b83e31b4b859fd43736a33e3dc7ba78807b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812429"
---
# <a name="activex-objects-for-print-web-pages"></a>打印网页的 ActiveX 对象





为打印网页提供了三个 ActiveX 对象： [Iasphelp](./iasphelp-automation-interface.md)、 [IOleCvt](./iolecvt-automation-interface.md)和 [ISNMP](./isnmp-automation-interface.md)。 ASP 文件可以使用脚本语言（如 VBScript）通过自动化接口访问每个对象。 对象和接口是在 Oleprn.dll 中实现的。

下面的列表包含每个接口的简要说明：

-   [Iasphelp 自动化接口](./iasphelp-automation-interface.md)允许你获取与指定打印机关联的属性。

    此接口提供对 ASP 会话变量中不可用的信息的访问权限，并允许 ASP 页获取与用于调用该页的打印机不同的信息。

-   [IOleCvt 自动化接口](./iolecvt-automation-interface.md)允许您将字符串从 ANSI 转换为 Unicode，反之亦然，将字符串转换为 UTF8 格式，并使用不同的代码页转换 Unicode 字符串。

-   如果打印机支持 RFC 1759， [ISNMP 自动化接口](./isnmp-automation-interface.md) 允许设置和检索与 SNMP oid 相关的值。

    [ISNMP](./isnmp-automation-interface.md)接口仅可用于使用 MICROSOFT 的 TCIP/IP 端口监视器的打印机。 此接口实质上是 SNMP 管理 API 函数的 OLE 自动化包装。 有关这些函数的详细信息，请参阅 Microsoft Windows SDK 文档。

    可以使用数字字符串指定 (Oid) 的对象 Id，以及为 RFC 1759 指定的管理信息库 (MIB) 包括文本名称字符串。 如 Windows SDK 文档中所述，可以使用其他 MIB 名称，如定义、编译和安装自定义的 Mib。

有关 ActiveX 和自动化的信息，请参阅 Windows SDK 文档。

 

