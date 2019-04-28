---
title: 打印网页的 ASP 变量
description: 打印网页的 ASP 变量
ms.assetid: eab0d5e0-0e20-443c-b714-a2b2327894e4
keywords:
- 自定义打印网页 WDK、 ASP 变量
- ASP 变量 WDK 打印机
- 会话变量 WDK 打印机
- 打印网页 WDK、 ASP 变量
- 网页 WDK 打印机，ASP 变量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e30b947bf0649a536a38e024981d6d409ead016
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331212"
---
# <a name="asp-variables-for-print-web-pages"></a>打印网页的 ASP 变量





Microsoft 提供一组 ASP 会话变量以供自定义打印网页。 下表列出了会话变量。 自定义的 ASP 文件不能修改这些变量。 如所述，某些变量的有效前提是 Microsoft 的 TCP/IP 端口监视器正用于打印机。

某些变量中作为会话变量传递，而其他参数传递中使用 URL 修饰。 可以使用会话访问会话变量 ("*VariableName*")。 可以使用请求访问的 URL 修饰符中传递的参数 ("*VariableName*")。 如果你想要自动刷新状态页，您可能会发现需 redecorate 页面所需的变量包含的 URL。 由于请求变量必须在 URL 中传递，它们可能需要编码和解码从 ANSI 转换为 Unicode 表示形式。 提供了帮助程序对象，其 COM ProgID 为"OlePrn.OleCvt"，用于启用编码和解码 URL 和 Unicode 中使用的 ANSI 之间。 此对象上的两种方法[ **IOleCvt::EncodeUnicodeName**](https://msdn.microsoft.com/library/windows/hardware/ff551829)，并[ **IOleCvt::DecodeUnicodeName**](https://msdn.microsoft.com/library/windows/hardware/ff551824)，可用于将翻译ANSI 到 Unicode，并从 Unicode 到 ANSI，分别。 此转换不需要执行的会话变量。

编码的变量值的 TCP/IP 端口变量？
仅监视？
类型 MS\_ASP1

初始的 Web 页，用于描述特定于打印机的详细信息的目录路径。

否

请求

否

MS\_社区

打印服务器的 SNMP 团体名称。

是

请求

否

MS\_计算机

打印服务器的计算机名称。

否

会议

否

MS\_DefaultPage

特定于打印机的详细信息的的默认 ASP 文件。

否

会议

否

MS\_设备

打印机的 SNMP 设备的索引。

是

请求

否

MS\_DHTMLEnabled

**TRUE**如果客户端支持动态 HTML; 否则为**FALSE**。

否

会议

否

MS\_IPAddress

打印机的 IP 地址。

是

请求

否

MS\_LocalServer

打印服务器的标识符。 这可能是 IP 地址或计算机名称。

否

会议

否

MS\_模型

打印机驱动程序的名称。

否

请求

是

MS\_Portname

打印机的端口名称。

否

请求

是

MS\_打印机

打印机的名称。

否

请求

是

MS\_SNMP

**TRUE**如果 SNMP 正在使用一台打印机，否则**FALSE**。

是

请求

否

MS\_URLPrinter

编码的 URL 格式中的打印机的名称。

否

请求

是

 

会话变量指定"当前"打印机，也就是说，对其调用 ASP 页打印机的属性。 若要获取对当前打印机，附加的打印机属性或获取属性的另一台打印机，请参阅[ActiveX 对象为打印 Web Pages](activex-objects-for-print-web-pages.md)。

 

 




