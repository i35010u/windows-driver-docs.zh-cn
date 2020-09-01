---
title: 打印网页的 ASP 变量
description: 打印网页的 ASP 变量
ms.assetid: eab0d5e0-0e20-443c-b714-a2b2327894e4
keywords:
- 自定义的打印网页 WDK，ASP 变量
- ASP 变量 WDK 打印机
- 会话变量 WDK 打印机
- 打印网页 WDK，ASP 变量
- 网页 WDK 打印机，ASP 变量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64cf038546ac01e01e942f85e02c1eb61b6b60f6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218270"
---
# <a name="asp-variables-for-print-web-pages"></a>打印网页的 ASP 变量





Microsoft 提供了一组 ASP 会话变量，供自定义的打印网页使用。 下表列出了会话变量。 自定义的 ASP 文件不能修改这些变量。 如上所述，某些变量仅在用于打印机的 Microsoft TCP/IP 端口监视器时有效。

某些变量作为会话变量传入，而其他变量则使用 URL 修饰传入。 会话变量可使用 Session ( "*VariableName*" ) 进行访问。 通过 URL 修饰传入的参数可通过使用请求 ( "*VariableName*" ) 进行访问。 如果希望自动刷新 "状态" 页，您可能会发现有必要用页面所需的变量 redecorate URL。 由于请求变量必须传入 URL，因此它们可能需要编码和解码才能从 ANSI 转换为 Unicode 表示形式。 提供了一个帮助器对象，其 COM ProgID 为 "OlePrn. OleCvt"，提供该对象以在 URL 中使用的 ANSI 和 Unicode 之间启用编码和解码。 此对象上的两个方法 [**IOleCvt：： EncodeUnicodeName**](./iolecvt-encodeunicodename.md)和 [**IOleCvt：:D ecodeunicodename**](./iolecvt-decodeunicodename.md)，可用于从 ANSI 转换为 Unicode，以及从 Unicode 转换为 ansi。 对于 Session 变量，无需执行此转换。

可变值 TCP/IP 端口变量已编码？
仅监视？
键入 MS \_ ASP1

用于描述特定于打印机的详细信息的初始网页的目录路径。

否

请求

否

MS \_ 社区

打印服务器的 SNMP 团体名称。

是

请求

否

MS \_ 计算机

打印服务器的计算机名称。

否

会话

否

MS \_ DefaultPage

用于特定于打印机的详细信息的默认 ASP 文件。

否

会话

否

MS \_ 设备

打印机的 SNMP 设备索引。

是

请求

否

MS \_ DHTMLEnabled

如果客户端支持动态 HTML，则为**TRUE** ;否则**为 FALSE**。

否

会话

否

MS \_ IPAddress

打印机的 IP 地址。

是

请求

否

MS \_ LocalServer

打印服务器的标识符。 这可能是 IP 地址或计算机名。

否

会话

否

MS \_ 模型

打印机驱动程序的名称。

否

请求

是

MS \_ portvalue

打印机的端口名称。

否

请求

是

MS \_ 打印机

打印机的名称。

否

请求

是

MS \_ SNMP

如果将 SNMP 与打印机一起使用，**则为 TRUE** ; 否则为**FALSE**。

是

请求

否

MS \_ URLPrinter

打印机的名称，采用编码的 URL 格式。

否

请求

是

 

Session 变量指定 "当前" 打印机的属性，即，为其调用 ASP 页的打印机。 若要获取当前打印机的其他打印机属性，或获取不同打印机的属性，请参阅 [用于打印网页的 ActiveX 对象](activex-objects-for-print-web-pages.md)。

 

