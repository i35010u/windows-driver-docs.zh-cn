---
title: 实现自定义 WMI 块
description: 实现自定义 WMI 块
keywords:
- WMI WDK 内核，事件块
- 事件块 WDK WMI
- 数据块 WDK WMI
- WMI WDK 内核，数据块
- 阻止 WDK WMI
- 自定义块 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3b322d6c188a1e420c737b3ef4edb7f8ebc1ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788667"
---
# <a name="implementing-custom-wmi-blocks"></a>实现自定义 WMI 块





驱动程序可以实现公开设备特定检测的 *自定义块* 。 例如，可报告温度的磁盘驱动器的驱动程序可能会实现自定义事件块，该事件块在驱动器温度超出安全阈值时通知 WMI 客户端。

若要实现自定义块，请执行以下操作：

-   在其 MOF 文件中定义类，将 MOF 文件编译为资源，并在驱动程序中包含资源，如 [发布 WMI 架构](publishing-a-wmi-schema.md)中所述。

-   在 [注册为 Wmi 数据提供程序](registering-as-a-wmi-data-provider.md)中所述，将块和驱动程序支持的其他标准和自定义块一起注册到 wmi。

-   处理所有 WMI 请求，这些请求在 **参数.** 数据路径中指定驱动程序的设备对象指针，并处理 **参数. wmi**[中的](handling-wmi-requests.md)标准块的 GUID。

驱动程序无法控制二进制 MOF 文件的加载顺序。 唯一的保证是在任何特定于驱动程序的 MOF 文件之前加载 wmicore。 因此，自定义 WMI 类只能从同一 MOF 文件或 wmicore 中的任何一个类继承。

若要提高自定义 WMI 数据块的性能和易用性，请考虑以下准则：

-   将正在操作的数据项置于同一数据块中。

    例如，i8042 端口控制器可能会维护有关键盘和鼠标端口的状态信息。 除了包含所有鼠标和键盘信息的单个大型数据块，驱动程序可能为鼠标端口定义一个数据块，并为键盘端口定义另一个数据块。

-   将经常使用的数据项置于不同的数据块中，特别是在其他情况下，它们将被分组为不常使用的项。

    例如，驱动程序可能会在包含单个项的数据块中公开 CPU 利用率，因此 WMI 客户端可以跟踪 CPU 利用率，而不会产生在块中检索其他数据项的开销。 WMI 客户端无法查询单个数据项，因此，若要获取一个项，则必须查询数据块的整个实例。

-   使用事件块通知 WMI 客户端异常事件，而不是替代错误日志记录。

    一次只能对有限数量的事件进行排队，并且如果队列为完整事件，将会丢失。 此外，无法保证将事件传递给 WMI 客户端的时间。

-   将事件块限制为最大大小1K 字节。

    事件项应定义为较小的数据类型，因为对于包含所生成事件的整个 [**WNODE \_ 事件 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item) 结构， (最初的 1k) 。 对于较大的通知，驱动程序可以发送 [**WNODE \_ 事件 \_ 引用**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference) 结构，该结构指定数据块的单个实例，然后 WMI 会通过查询来获取实际事件。 但是，这会增加发生事件和通知之间的时间延迟。

-   将固定大小的数据项置于数据块的开头，后跟任意可变大小的数据项。

    例如，具有三个 DWORD 数据项和一个可变长度字符串的数据块应该首先放入三个 Dword，然后放入字符串。 在块的开始处放置固定大小的数据项，将允许 WMI 客户端更轻松地提取它们。

-   考虑要访问驱动程序数据块的系统用户的类型。 系统为所有 WMI 类 Guid 提供默认安全描述符。 如果需要，可以在设备的 INF 文件中提供备用的安全描述符。 有关详细信息，请参阅 [创建安全设备安装](../install/creating-secure-device-installations.md)。

WMI 不支持版本控制，因此驱动程序编写器必须定义新的 MOF 类，并生成新的 GUID 来修改现有的自定义块。

 

