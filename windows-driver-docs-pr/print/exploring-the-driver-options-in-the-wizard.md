---
title: 浏览向导中的驱动程序选项
description: 本主题将探讨 "创建 v4 打印驱动程序向导" 的第一部分中的驱动程序选项。
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: ca43bb364cade8d05356d8398621cd520d444013
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797101"
---
# <a name="exploring-the-driver-options-in-the-wizard"></a>浏览向导中的驱动程序选项

本主题将探讨 " **创建 V4 打印驱动程序** 向导" 的第一部分中的驱动程序选项。

此处提供的信息以汇总形式提供，有助于快速了解各种功能选项。 如果需要有关任何功能的详细信息，请按照提供的相关主题的链接，这些主题提供更多详细信息。

## <a name="driver-rendering-type"></a>驱动程序呈现类型

### <a name="v4-print-driver-with-custom-rendering-filters-accepts-xps-only"></a>V4 打印驱动程序与自定义呈现筛选器 (仅接受 XPS) 

如果要创建仅接受 Microsoft XPS 格式作为输入的打印机驱动程序，请选择此选项。 请注意，此驱动程序可以生成 XPS 和/或 OpenXPS 格式的输出，具体取决于在 " **选择驱动程序 XPS 格式** " 字段中所做的选择。

### <a name="v4-print-driver-with-class-driver-rendering"></a>V4 打印驱动程序与类驱动程序呈现

如果选择此选项，则将创建一个打印机驱动程序，该驱动程序可以接受 XPS 或 OpenXPS 格式的输入。 此外，当您选择此驱动程序时，您必须在此向导的下一页上指示您要用于呈现的打印类驱动程序的名称。

### <a name="microsoft-xps-to-pcl6-render-filter-accepts-xps-only"></a>Microsoft XPS 到 PCL6 render 筛选器 (仅接受 XPS) 

使用此选项可以创建仅接受 XPS 格式作为输入的筛选器驱动程序模块，并将输入转换为 PCL6。 请注意，此驱动程序可以生成 XPS 和/或 OpenXPS 格式的输出，具体取决于在 " **选择驱动程序 XPS 格式** " 字段中所做的选择。

### <a name="microsoft-xps-to-postscript-render-filter-accepts-xps-only"></a>Microsoft XPS 到 PostScript render 筛选 (仅接受 XPS) 

使用此选项可以创建仅接受 XPS 格式作为输入的筛选器驱动程序模块，并将输入转换为 PostScript。 请注意，此驱动程序可以生成 XPS 和/或 OpenXPS 格式的输出，具体取决于在 " **选择驱动程序 XPS 格式** " 字段中所做的选择。

## <a name="driver-xps-format"></a>驱动程序 XPS 格式

### <a name="xps"></a>XPS

此选项将驱动程序配置为仅生成 XPS 格式的输出。

### <a name="openxps"></a>OpenXPS

此选项将驱动程序配置为仅生成 OpenXPS 格式的输出。

### <a name="xps-openxps"></a>XPS、OpenXPS

此选项将驱动程序配置为生成 XPS 或 OpenXPS 格式的输出，在 INF 文件中，将 XPS 设置为默认值。

### <a name="openxps-xps"></a>OpenXPS、XPS

此选项将驱动程序配置为以 OpenXPS 或 XPS 格式生成输出，并将 OpenXPS 设置为 INF 文件中的默认值。

## <a name="driver-configuration-type"></a>驱动程序配置类型

### <a name="gpd-driver"></a>GPD 驱动程序

此选项将使向导使用打印机驱动程序 (GPD) 语言文件创建通用打印机说明。

### <a name="ppd-driver"></a>PPD 驱动程序

此选项将使向导使用打印机驱动程序 (PPD) 语言文件创建 PostScript 打印机说明。

## <a name="protected-printing"></a>受保护打印

### <a name="enable-protected-printing"></a>启用受保护打印

如果希望能够使用 PIN 锁定发送到打印机的打印请求，请选择此选项。 然后，最终用户必须在打印机上提供相同的 PIN 才能发布锁定的打印请求以进行打印。 有关详细信息，请参阅 [受保护打印的驱动程序支持](driver-support-for-protected-printing.md)。

## <a name="additional-functionality"></a>附加功能

### <a name="driver-property-bag"></a>驱动程序属性包

这是一个描述驱动程序属性包内容的 XML 文件。 此文件中指定的属性以及添加到项目的 ByteArray 或 IStream 文件夹的任何数据文件中提供的信息将编译到驱动程序属性包中。 有关详细信息，请参阅 [V4 打印机驱动程序属性包](v4-driver-property-bags.md)。

您可以在 Windows 驱动程序工具包的 "此文件夹： *\\ 包括 \\ um \\printdriverproperties.xml* 中找到驱动程序属性包模板的 XML 架构。

### <a name="driver-event-file"></a>驱动程序事件文件

此文件用于描述应导致引发驱动程序事件的双向查询和触发器。 请注意，驱动程序事件仅支持标准字符串。 有关驱动程序事件和标准字符串的详细信息，请参阅 [自定义 UI 的驱动程序支持](driver-support-for-customized-ui.md)。

### <a name="devmode-mapping-file"></a>DevMode 映射文件

这是一个 XML 文件，与 JavaScript 代码中的 PrintTicket < > DEVMODE 转换一起使用。 提供此文件时，必须在 [V4 驱动程序清单](v4-driver-manifest.md)中指定该文件。

### <a name="queue-property-bag"></a>队列属性包

此模板允许你提供按队列配置设置，包括送纸器映射和打印机属性（如可安装选项）的配置。 有关详细信息，请参阅 [V4 打印机驱动程序属性包](v4-driver-property-bags.md)。

### <a name="resource-dll"></a>资源 DLL

此模板允许你提供资源说明，例如外部存储的字体、图标和其他位图，以及可本地化的用户界面文本字符串。 有关详细信息，请参阅 [在微型驱动程序中使用资源 dll](using-resource-dlls-in-a-minidriver.md)、 [V4 驱动程序清单](v4-driver-manifest.md) 和 [v4 打印机驱动程序本地化](v4-driver-localization.md)。

### <a name="constraints-js"></a>约束 JS

此模板提供所有支持的 JavaScript 约束入口点的方法标头。 有关详细信息，请参阅 [JavaScript 约束](javascript-constraints.md)。

### <a name="autoconfiguration-gdl"></a>自动配置 GDL

这为 v4 打印驱动程序提供了一个基本的自动配置文件。 有关自动配置的 GDL 语法的信息，以及要浏览示例文件的信息，请参阅 [打印自动配置示例](/samples/microsoft/windows-driver-samples/print-auto-configuration-sample)。

### <a name="tcpmon-bidi-extension-xml"></a>TCPMon 双向扩展 XML

这提供了一个简单的 TCP/IP 双向扩展文件。 有关标准 TCP/IP 端口监视器的双向语法的详细信息，请参阅 [Tcp/ip 架构扩展](tcp-ip-schema-extensions.md)。

### <a name="wsdmon-bidi-extension-xml"></a>WSDMon 双向扩展 XML

这提供了一个简单的 WSD 双向扩展文件。 有关 WSDMon 的双向语法的详细信息，请参阅 [WSD 架构扩展](wsd-schema-extensions.md)。

### <a name="usbmon-bidi-extension-xml--js"></a>USBMon 双向扩展 XML + JS

这提供了一个简单的 USB 双向扩展文件。 它依赖于是否存在匹配的 USB 双向扩展器 JavaScript。 有关详细信息，请参阅 [USB 双向扩展](usb-bidi-extender.md)器。
