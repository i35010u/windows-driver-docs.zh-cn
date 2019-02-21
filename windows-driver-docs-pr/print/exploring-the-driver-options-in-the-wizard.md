---
title: 浏览向导中的驱动程序选项
description: 本主题探讨创建 v4 打印驱动程序向导的第一个部分中的驱动程序选项。
ms.assetid: 48FF0A37-BBAF-49D1-9BDE-128AED00BEEF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ae6638618596c5fc88c1d222ec07f8593b41614
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526014"
---
# <a name="exploring-the-driver-options-in-the-wizard"></a>浏览向导中的驱动程序选项


本主题探讨创建 v4 打印驱动程序向导的第一个部分中的驱动程序选项。

在汇总窗体，以帮助您快速找出有关各种功能选项此处提供的信息。 如果要了解有关任何功能的详细信息，提供更多详细信息的相关主题按照提供的链接。

## <a name="driver-rendering-type"></a>驱动程序呈现类型


V4 打印驱动程序和自定义呈现的筛选器 （仅接受 XPS）

如果你想要创建只接受作为输入的 Microsoft XPS 格式的打印机驱动程序，请选择此选项。 请注意，此驱动程序可以生成 XPS 和/或 OpenXPS 格式，具体取决于你在中进行选择的输出**选择驱动程序 XPS 格式**字段。
V4 打印驱动程序和类驱动程序呈现

如果选择此选项，您创建可接受 XPS 或 OpenXPS 格式的输入的打印机驱动程序。 此外，当您选择此驱动程序时，必须以指示你想要用于呈现打印类驱动程序的名称此向导的下一页上。
Microsoft XPS 到 PCL6 呈现 （仅接受 XPS） 的筛选器

此选项可以创建一个筛选器驱动程序模块仅接受 XPS 格式作为输入，并将输入转换 PCL6 为。 请注意，此驱动程序可以生成 XPS 和/或 OpenXPS 格式，具体取决于你在中进行选择的输出**选择驱动程序 XPS 格式**字段。
Microsoft XPS 到 PostScript 呈现 （仅接受 XPS） 的筛选器

此选项可以创建一个筛选器驱动程序模块仅接受 XPS 格式作为输入，并将转换后脚本的输入。 请注意，此驱动程序可以生成 XPS 和/或 OpenXPS 格式，具体取决于你在中进行选择的输出**选择驱动程序 XPS 格式**字段。
## <a name="driver-xps-format"></a>驱动程序 XPS 格式


XPS

此选项配置驱动程序以生成输出中仅 XPS 格式。
OpenXPS

此选项配置要在仅 OpenXPS 格式中生成输出的驱动程序。
XPS OpenXPS

此选项配置驱动程序以使用 XPS INF 文件中设置为默认值生成以 XPS 或 OpenXPS 格式输出。
OpenXPS XPS

此选项配置驱动程序以使用 OpenXPS INF 文件中设置为默认值生成 OpenXPS 或 XPS 格式的输出。
## <a name="driver-configuration-type"></a>驱动程序配置类型


GPD 驱动程序

此选项将导致向导以使用打印机驱动程序创建通用打印机说明 (GPD) 语言文件。
PPD 驱动程序

此选项将导致向导以使用打印机驱动程序创建 PostScript 打印机说明 (PPD) 语言文件。
## <a name="protected-printing"></a>受保护的打印


启用受保护的打印

选择此选项，如果您希望能够使用 PIN 锁定发送到打印机的打印请求。 然后，最终用户必须提供相同的 PIN 在打印机释放锁定的打印请求进行打印。 有关详细信息，请参阅[针对受保护的打印驱动程序支持](driver-support-for-protected-printing.md)。
## <a name="additional-functionality"></a>附加功能


驱动程序属性包

这是一个 XML 文件，描述驱动程序属性包的内容。 此文件，以及添加到项目的 ByteArray 或 IStream 文件夹的任何数据文件中提供的信息中指定的属性将编译到驱动程序属性包。 有关详细信息，请参阅[V4 打印机驱动程序属性包](v4-driver-property-bags.md)。

和您可以找到 XML 架构的驱动程序属性包模板在 Windows 驱动程序工具包中，此文件夹中：*\\包括\\um\\printdriverproperties.xml*。

驱动程序事件文件

此文件用于描述 Bidi 查询和触发器的会导致驱动程序事件被引发。 而且，务必要注意的事件驱动程序仅支持标准字符串。 有关驱动程序的事件和标准字符串的详细信息，请参阅[驱动程序支持自定义 UI](driver-support-for-customized-ui.md)。
DevMode 映射文件

这是一个 XML 文件，可与 PrintTicket &lt; - &gt; DEVMODE 转换中的 JavaScript 代码。 当你提供此文件时，它必须以指定[V4 驱动程序清单](v4-driver-manifest.md)。
队列属性包

此模板允许你提供每个队列配置设置，包括送纸器窗体映射和打印机属性，如可安装选项的配置。 有关详细信息，请参阅[V4 打印机驱动程序属性包](v4-driver-property-bags.md)。
资源 DLL

此模板允许你提供的资源，例如外部存储的字体、 图标和其他位图和可本地化的用户界面文本字符串说明。 有关详细信息，请参阅[微型驱动程序中使用资源 Dll](using-resource-dlls-in-a-minidriver.md)， [V4 驱动程序清单](v4-driver-manifest.md)并[V4 打印机驱动程序本地化](v4-driver-localization.md)。
约束 JS

此模板提供了所有受支持的 JavaScript 约束入口点的方法标头。 有关详细信息，请参阅[JavaScript 约束](javascript-constraints.md)。
自动配置 GDL

这为 v4 打印驱动程序提供基本的自动配置文件。 有关 GDL 语法，用于自动配置，以及浏览一个示例文件的信息，请参阅[打印自动配置示例](https://go.microsoft.com/fwlink/p/?LinkId=617938)。
TCPMon Bidi 扩展 XML

这提供了一个简单的 TCP/IP Bidi 扩展文件。 为标准 TCP/IP 端口监视器 Bidi 语法的详细信息，请参阅[TCP/IP 架构扩展](tcp-ip-schema-extensions.md)。
WSDMon Bidi 扩展 XML

这提供了一个简单的 WSD Bidi 扩展文件。 有关 WSDMon Bidi 语法的详细信息，请参阅[WSD 架构扩展](wsd-schema-extensions.md)。
USBMon Bidi 扩展 XML + JS

这提供了一个简单的 USB Bidi 扩展文件。 它所依赖的匹配的 USB Bidi 扩展器 JavaScript 存在。 有关详细信息，请参阅[USB Bidi 扩展器](usb-bidi-extender.md)。
 

 




