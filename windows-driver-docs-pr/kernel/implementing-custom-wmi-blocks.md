---
title: 实现自定义 WMI 块
description: 实现自定义 WMI 块
ms.assetid: c596924f-9f82-4ca7-b0f0-afc596d7bf99
keywords:
- WMI WDK 内核，事件块
- 事件阻止 WDK WMI
- 数据将阻止 WDK WMI
- WMI WDK 内核，数据块
- 块 WDK WMI
- 自定义块 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 808fe8aeb00c8b711885285ee2f7c1b3f021ae78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524896"
---
# <a name="implementing-custom-wmi-blocks"></a>实现自定义 WMI 块





驱动程序可以实现*自定义块*公开特定于设备的检测。 例如，可以报告温度的磁盘驱动器的驱动程序可能会实现驱动器的温度超出安全阈值时通知 WMI 客户端的自定义事件块。

若要实现自定义块，驱动程序：

-   在其 MOF 文件中定义的类、 编译 MOF 文件转换为资源和在驱动程序中包括的资源，如中所述[发布 WMI 架构](publishing-a-wmi-schema.md)。

-   块向注册 WMI 除了驱动程序，支持的其他标准和自定义块中所述[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

-   处理指定驱动程序的设备对象指针上的所有 WMI 请求**Parameters.WMI.ProviderId**和处的标准块 GUID **Parameters.WMI.DataPath**中所述，[处理 WMI 请求](handling-wmi-requests.md)。

驱动程序不能控制二进制 MOF 文件的加载的顺序。 只能保证是该 wmicore.mof 先加载前，任何特定于驱动程序的 MOF 文件。 因此，仅必须从在相同的 MOF 文件中，或在 wmicore.mof 任一类继承自定义 WMI 类。

若要提高性能和易用性的自定义 WMI 数据块，请考虑以下准则：

-   将汇总到同一个数据块中的操作状态分组的数据选项。

    例如，i8042 端口控制器可能会维护有关键盘和鼠标端口的状态信息。 而不是包含所有鼠标和键盘信息的单个大型数据块，驱动程序可能会定义一个数据块为鼠标端口和键盘端口的另一个数据块。

-   Put 经常使用单独的数据块中的数据项，尤其是当它们将否则与分组在一起不常使用的项。

    例如，驱动程序可能会公开具有单个项的数据块中的 CPU 使用率，因此，WMI 客户端无法跟踪 CPU 利用率，而不会产生检索其他数据块中的项的开销。 WMI 客户端无法查询单个数据项，因此若要获取一项它必须查询整个数据块的实例。

-   使用事件块的异常事件的 WMI 客户端通知不作为错误日志记录的替代方法。

    可以一次排队有限的数量的事件，如果队列已满事件都将丢失。 此外，无法保证事件传送到 WMI 客户端的时间。

-   限制事件块的最大大小为 1k 字节。

    应为较小的数据类型时，定义事件项目，因为注册表定义的大小限制 (最初，1 K) 的整个[ **WNODE\_事件\_项**](https://msdn.microsoft.com/library/windows/hardware/ff566373)结构包含生成的事件。 对于大型的通知，驱动程序可以发送[ **WNODE\_事件\_引用**](https://msdn.microsoft.com/library/windows/hardware/ff566374)结构，它指定 WMI 然后查询以获取一个数据块的单个实例实际事件。 但是，这会增加之间的匹配项的事件和通知的时间间隔。

-   将固定大小的数据项目放置在数据块，然后对任何大小可变的数据项开头。

    例如，数据块，有三个 DWORD 数据项目，一个可变长度字符串应将三个 dword 值第一次，跟的字符串。 将固定大小的数据的项放在块的开头允许 WMI 客户端能够更轻松地将其提取。

-   请考虑哪些类型的系统用户想要访问您的驱动程序的数据块。 系统提供的默认安全描述符的所有 WMI 类的 Guid。 如有必要，可以提供备用的安全描述符中设备的 INF 文件。 有关详细信息，请参阅[创建安全的设备安装](https://msdn.microsoft.com/library/windows/hardware/ff540212)。

WMI 不支持此功能，因此驱动程序编写器必须定义一个新的 MOF 类，并生成新的 GUID，若要修改现有的自定义块。

 

 




