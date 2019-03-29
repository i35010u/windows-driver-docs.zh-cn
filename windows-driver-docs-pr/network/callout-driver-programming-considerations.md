---
title: 标注驱动程序编程注意事项
description: 标注驱动程序编程注意事项
ms.assetid: e470202a-bc3b-41ac-8156-8aac8cd976cd
keywords:
- Windows 筛选平台标注驱动程序 WDK，编程注意事项
- 标注驱动程序 WDK Windows 筛选平台，编程注意事项
- 建立 ALE 流量筛选层 WDK Windows 筛选平台
- 内核模式标注驱动程序 WDK Windows 筛选平台
- 用户模式下标注驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b71ca15eb81e6704484a734f9e42e159282587c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562218"
---
# <a name="callout-driver-programming-considerations"></a>标注驱动程序编程注意事项


编程 Windows 筛选平台标注驱动程序时，请考虑以下主题。

### <a href="" id="user-mode-vs--kernel-mode"></a>用户模式与。内核模式

如果所需的筛选可以执行此操作通过使用标准筛选功能内置于 Windows 筛选平台，独立软件供应商 (Isv) 应编写用户模式下配置而不是筛选器引擎的管理应用程序编写内核模式标注驱动程序。 必须处理方式不能由标准的内置筛选功能的网络数据时，应仅编写一个内核模式标注驱动程序。 有关如何编写在用户模式 Windows 筛选平台管理应用程序的信息，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK 中的文档。

### <a name="choice-of-filtering-layer"></a>所选的筛选层

标注驱动程序应筛选在网络堆栈中最高可能筛选层的网络数据。 例如，如果所需的筛选任务可以在流层处理，它不应实现在网络层上。 您的驱动程序应使用以保证兼容性与在 Windows 中的 IPsec 筛选层建议详细信息，请参阅[开发 IPsec 兼容标注驱动程序](developing-ipsec-compatible-callout-drivers.md)。

### <a href="" id="blocking-at-the-application-layer-enforcement--ale--flow-established-l"></a>阻止在应用程序层强制 (ALE) 流建立层

通常情况下，一个标注如果已添加到在其中一个筛选器引擎*ALE 流建立*筛选层 (FWPM\_层\_ALE\_流\_已建立\_V4或 FWPM\_层\_ALE\_流\_已建立\_V6)，将其[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数应永远不会返回 FWP\_操作\_阻止的操作。 决策进行授权或拒绝不应在其中一个 ALE 流执行的连接建立筛选层。 在其他 ALE 筛选层之一应始终将此类决策。

对这些产品的唯一正当理由[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数以返回 FWP\_操作\_阻止该操作是如果发生错误，可能会造成一些潜在的安全风险如果已建立的连接未结束。 在这种情况下，返回 FWP\_操作\_阻止的操作将关闭连接以防止潜在的安全风险被利用。

### <a name="callout-function-execution-time"></a>标注函数执行时间

因为筛选器引擎通常会标注的标注函数调用在 IRQL = 调度\_级别，请确保这些函数以保持系统高效地运行尽可能快地完成其执行。 扩展执行在 IRQL = 调度\_级别可以对系统的整体性能产生负面影响。

### <a name="injecting-into-the-receive-data-path"></a>将注入到接收的数据路径

它们调用之前，标注应重新计算校验和 IP[数据包注入函数](packet-injection-functions.md)因为原始数据包中的校验和可能不会正确数据包重组从 IP 的注入到接收数据路径数据包片段。 没有可靠的机制，该值指示是否从片段重组 net 缓冲区列表。

### <a name="inline-injection-of-tcp-packet-from-transport-layers"></a>从传输层的 TCP 数据包的内联注入

由于 TCP 堆栈的锁定行为，在传输层标注无法插入新的或克隆 TCP 数据包[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)标注函数。 如果需要内联注入，标注必须排队 DPC 执行注入。

### <a name="outgoing-ip-header-alignment"></a>传出 IP 标头的对齐方式

介绍 net 缓冲区列表中的 IP 标头 MDL ([**NET\_缓冲区\_当前\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff568379)([**NET\_缓冲\_列表\_第一个\_NB**](https://msdn.microsoft.com/library/windows/hardware/ff568394)(*netBufferList*))) 必须是指针对齐时之一[数据包注入函数](packet-injection-functions.md)用于将数据包数据注入到传出路径。 因为可能的传入数据包 IP 标头 MDL 指针对齐，标注必须重新生成 IP 标头 （如果尚不存在对齐） 时将传入数据包注入到传出路径。

## <a name="related-topics"></a>相关主题


[Windows 筛选平台标注驱动程序](windows-filtering-platform-callout-drivers2.md)

 

 






