---
description: Microsoft 提供了一组专用设备类和 USB 描述符，它们被称为 Microsoft OS 描述符 (MODs) 。
title: 针对 USB 设备的 Microsoft OS 描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3398892651089a1b4f41eeea8e27b6a59ba5973e
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009861"
---
# <a name="microsoft-os-descriptors-for-usb-devices"></a>针对 USB 设备的 Microsoft OS 描述符


**摘要**

-   [Microsoft OS 1.0 描述符规范](./microsoft-os-1-0-descriptors-specification.md)
-   [Microsoft OS 2.0 描述符规范](./microsoft-os-2-0-descriptors-specification.md)

Microsoft 提供了一组专用设备类和 USB 描述符，它们被称为 Microsoft OS 描述符 (MODs) 。




由于包含多个硬件功能的设备的快速出现，许多制造商发现，其设备不能轻松地进入任何当前的通用串行总线 (USB) 设备类中。 这情况下了一种最引人注目的 USB 技术功能的制造商：根据设备) 的类别 (的驱动程序软件标准化。 Microsoft Windows 为大多数属于标准 USB 设备类的设备提供本机类驱动程序，并且这些驱动程序允许最终用户轻松地将此类设备连接到计算机，而无需安装特殊软件。

为了适应其设备不适合当前 USB 设备类集的制造商，Microsoft Corporation 已开发了一组专用设备类和 USB 描述符，它们被称为 Microsoft OS 描述符 (MODs) 。 应用程序和系统软件都可以通过查询设备来确定是否支持 MODs 来识别属于 Microsoft 定义的设备类的设备。

Microsoft OS 描述符除了支持专用设备类之外，还有重要的使用。 特别是，它们提供了一种机制，用于从设备固件派生最大权益。 利用 Microsoft OS 描述符的帮助，你可以使用该固件提供帮助文件、特殊图标、统一资源定位符 (Url) 、注册表设置，以及简化安装和提高客户满意度所需的其他数据。 在某些情况下，可以放弃存储媒体（如软盘和 Cd），从而简化对升级的交付和支持。

## <a name="operating-system-support"></a>操作系统支持


支持 Microsoft OS 1.0 描述符：

-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista 和 Windows Server 2008
-   Windows XP Service Pack 1 (SP1) 、Windows Server 2003

支持 Microsoft OS 2.0 描述符：

-   Windows 8.1

## <a name="why-does-windows-issue-a-string-descriptor-request-to-index-0xee"></a>为什么 Windows 发出字符串描述符请求来索引0xEE？


支持 Microsoft OS 描述符的设备必须在0xEE 的固定字符串索引处的固件中存储特殊的 USB 字符串描述符。 此字符串描述符称为 "Microsoft 操作系统字符串描述符"。

-   它的状态表明设备包含一个或多个 OS 功能描述符。
-   它包含检索关联的 OS 功能描述符所需的数据。
-   它包含一个签名字段，该字段将 OS 字符串描述符与 Ihv 可能选择在0xEE 中存储的其他字符串区分开来。
-   它包含一个版本号，该版本号允许将来的 Microsoft OS 描述符的修订版。

如果0xEE 上没有字符串说明符，或该索引处的字符串描述符不是有效的 OS 字符串描述符，则 Windows 将假定该设备不包含任何 OS 功能描述符。

首次将新设备连接到计算机时，支持 Microsoft 操作系统描述符的操作系统将请求索引0xEE 处的字符串描述符。 Microsoft OS 字符串描述符包含一个嵌入的签名字段，操作系统使用该字段将其与其他可能位于索引0xEE 的字符串区分开来。 存在字符串描述符，其中包含索引0xEE 处的正确签名字段向操作系统指示设备支持 Microsoft OS 描述符。 Microsoft 操作系统字符串描述符还向操作系统提供版本信息。

在设备枚举过程中，操作系统会在设备枚举过程中查询索引0xEE 处的字符串描述符，这可能会导致某些设备出现故障。 支持 Microsoft 操作系统描述符的 Windows 操作系统版本不支持此类设备。

如果设备在索引0xEE 处不包含有效的字符串描述符，则它必须使用隔栏数据包进行响应 (换言之，一个数据包包含类型为 "延迟" 的数据包标识符) ，这在通用串行总线规范的 "请求错误" 一节中进行了介绍。 如果设备未使用隔间的数据包进行响应，系统将向设备发出单结束的零重置数据包，以帮助其从其停止状态恢复 (仅) Windows XP。

操作系统从设备请求 Microsoft OS 字符串描述符后，将创建以下注册表项：

**HLKM \\ SYSTEM \\ CurrentControlSet \\ Control \\ UsbFlags \\ * vvvvpppprrrrr***

操作系统在此注册表项下创建名为 **osvc**的注册表项，该注册表项指示设备是否支持 Microsoft OS 描述符。 如果设备在第一次为 Microsoft OS 字符串描述符查询它时未提供有效的响应，则操作系统将不会对该描述符进行进一步的请求。

有关该注册表项下的注册表项，请参阅 [USB 设备注册表项](usb-device-specific-registry-settings.md)。

有关其他信息，请参阅 [MICROSOFT OS 描述符](./microsoft-os-1-0-descriptors-specification.md)。

## <a name="what-types-of-os-feature-descriptors-are-supported-by-windows"></a>Windows 支持哪种类型的操作系统功能描述符？


作为功能描述符存储的任何信息都必须符合 Microsoft 已定义的标准格式之一。 在没有 Microsoft 同意的情况下，不能定义或实现其他功能描述符。 Microsoft 定义了以下功能描述符：

-   **扩展的兼容 ID**。 Windows 使用类和子类代码来帮助找到 USB 设备的相应默认驱动程序。 但是，USB 设备工作组必须分配这些代码。 这意味着实现新功能类型的设备通常还没有适当的类和子类代码，因此 Windows 无法使用这些代码来选择默认驱动程序。 Ihv 可以通过将固件中的信息存储为扩展的兼容 ID OS 功能描述符来规避此问题。 然后，Windows 可以在设备接通电源时检索此信息，并使用它来帮助确定要加载的默认驱动程序。
-   **扩展属性**。 目前，可以在两个级别为 USB 设备声明属性：类级别或 devnode 级别。 扩展属性 OS 功能描述符允许供应商存储设备固件中的其他属性（如帮助页、Url 和图标）。

## <a name="related-topics"></a>相关主题
[Microsoft OS 1.0 描述符规范](./microsoft-os-1-0-descriptors-specification.md)  
[Microsoft OS 2.0 描述符规范](./microsoft-os-2-0-descriptors-specification.md)  
[为 Windows 构建 USB 设备](building-usb-devices-for-windows.md)