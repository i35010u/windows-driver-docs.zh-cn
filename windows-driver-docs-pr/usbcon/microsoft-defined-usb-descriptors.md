---
Description: Microsoft provides a set of proprietary device classes and USB descriptors, which are called Microsoft OS Descriptors (MODs).
title: Microsoft 操作系统描述符的 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d08d4c9850338fc9e23ca57c2f61d3864fd513e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520945"
---
# <a name="microsoft-os-descriptors-for-usb-devices"></a>Microsoft 操作系统描述符的 USB 设备


**摘要**

-   [1.0 的 Microsoft 操作系统描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617154)
-   [2.0 的 Microsoft 操作系统描述符规范](https://go.microsoft.com/fwlink/p/?linkid=306681)

Microsoft 提供了一套专有设备类和 USB 描述符，它称为 Microsoft OS 描述符 （模式）。




包含多个硬件功能的设备的快速兴起，由于许多制造商发现，他们的设备执行操作不完全适合于到任何当前的通用串行总线 (USB) 设备类。 这 deprives 此类制造商的 USB 技术的最具吸引力的功能之一: （根据设备的类） 的驱动程序软件的标准化。 Microsoft Windows 的大部分属于标准 USB 设备类的设备提供本机类驱动程序，并且这些驱动程序允许最终用户能够轻松地将此类设备连接到计算机而无需安装特殊软件。

以适应其设备执行不适合当前组 USB 设备类的制造商，Microsoft Corporation 开发了一套专有设备类和 USB 描述符，它称为 Microsoft OS 描述符 （模式）。 应用程序和系统软件可以标识属于 Microsoft 定义的设备类通过查询以确定它们是否支持模式的设备的设备。

Microsoft OS 描述符具有不支持的专有设备类的重要用途。 具体而言，它们提供用于派生自设备固件的最大的好处的机制。 Microsoft OS 描述符的帮助下，可以使用固件将帮助文件、 特殊的图标、 统一资源定位器 (Url)、 注册表设置和其他数据的需要来简化安装，并提高客户满意度。 在某些情况下，可以放弃 CDs-软盘等的存储介质，它简化了交付与支持的升级。

## <a name="operating-system-support"></a>操作系统支持


支持 Microsoft 操作系统 1.0 描述符：

-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista、 Windows Server 2008
-   Windows XP Service Pack 1 (SP1)，Windows Server 2003

支持 Microsoft 操作系统 2.0 描述符：

-   Windows 8.1

## <a name="why-does-windows-issue-a-string-descriptor-request-to-index-0xee"></a>为什么 Windows Does 向索引 0xEE 发出字符串描述符请求？


支持 Microsoft 操作系统描述符的设备必须在 0xEE 的固定的字符串的索引处的固件中存储一个特殊的 USB 字符串描述符。 此字符串描述符称为 Microsoft 操作系统字符串描述符。

-   它的存在指示设备包含一个或多个操作系统功能描述符。
-   它包含检索关联的操作系统功能描述符所需的数据。
-   它包含用于 OS 字符串描述符与 Ihv 可能会选择可以在 0xEE 存储其他字符串区分开来的签名字段。
-   它包含用于 Microsoft 操作系统描述符的未来版本的版本号。

如果在 0xEE，没有字符串描述符，或者在该索引处的字符串描述符不是有效的 OS 字符串描述符，Windows 会假定设备不包含任何操作系统功能描述符。

当第一次将新设备连接到计算机中时，支持 Microsoft 操作系统描述符的操作系统将请求 0xEE 索引处的字符串描述符。 Microsoft 操作系统字符串描述符包含操作系统用于区别于其他字符串的位置索引 0xEE 可能是一个嵌入式的签名字段。 包含索引 0xEE 处的正确的签名字段的字符串描述符存在向操作系统指示设备支持在 Microsoft OS 描述符。 Microsoft 操作系统字符串描述符还提供了操作系统的版本信息。

设备在枚举过程-之前加载设备驱动程序-这可能会导致某些设备无法正常工作的 0xEE 索引处的字符串描述符操作系统查询。 此类设备不受支持 Microsoft 操作系统描述符的 Windows 操作系统版本。

如果设备不包含在索引 0xEE 的有效字符串描述符，它必须响应停滞数据包 （换而言之，数据包包含数据包标识符的类型停滞），这通用串行总线的"请求错误"部分中所述规范。 如果设备没有响应与停滞数据包，系统将发出一个结束零个重置数据包到设备，以帮助其从其已停止状态 (仅适用于 Windows XP) 中恢复。

操作系统从设备请求 Microsoft 操作系统字符串描述符后，将创建以下注册表项：

**HLKM\\SYSTEM\\CurrentControlSet\\Control\\UsbFlags\\*vvvvpppprrrrr***

操作系统会创建一个名为的注册表项**osvc**，指示设备是否支持 Microsoft 操作系统描述符此注册表项下。 如果设备不提供有效响应第一个时间，操作系统查询其用于 Microsoft 操作系统字符串描述符，操作系统将使该描述符没有更多请求。

有关该注册表项下的注册表项，请参阅[USB 设备注册表条目](usb-device-specific-registry-settings.md)。

有关其他信息，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=617154)。

## <a name="what-types-of-os-feature-descriptors-are-supported-by-windows"></a>Windows 支持哪些类型的操作系统功能描述符？


要存储功能描述符必须遵守 Microsoft 已定义的标准格式之一的任何信息。 不能定义或未经 Microsoft 同意实现其他功能描述符。 Microsoft 还定义了以下功能描述符：

-   **扩展兼容 ID**。 Windows 使用类和子类代码来帮助找到 USB 设备的适当的默认驱动程序。 但是，USB 设备 Working Group 必须分配这些代码。 这意味着，通常实现的功能的新类型的设备还没有相应的类和子类代码，因此 Windows 不能使用代码来选择默认的驱动程序。 Ihv 可以避开此问题，通过为扩展的兼容 ID 操作系统功能描述符的固件中存储的信息。 然后，Windows 可以在插入设备时检索此信息，并使用它来帮助确定要加载的默认驱动程序。
-   **扩展属性**。 目前，有两个级别的属性可以声明为 USB 设备： 类级别或 devnode 级别。 操作系统功能描述符允许存储其他属性-如一位供应商的扩展的属性帮助页、 Url 和图标中设备固件。

## <a name="related-topics"></a>相关主题
[1.0 的 Microsoft 操作系统描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617154)  
[2.0 的 Microsoft 操作系统描述符规范](https://go.microsoft.com/fwlink/p/?linkid=306681)  
[针对 Windows 构建的 USB 设备](building-usb-devices-for-windows.md)  



