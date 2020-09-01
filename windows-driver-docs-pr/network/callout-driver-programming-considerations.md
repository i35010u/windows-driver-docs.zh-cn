---
title: 标注驱动程序编程注意事项
description: 标注驱动程序编程注意事项
ms.assetid: e470202a-bc3b-41ac-8156-8aac8cd976cd
keywords:
- Windows 筛选平台标注驱动程序 WDK，编程注意事项
- 标注驱动程序 WDK Windows 筛选平台，编程注意事项
- ALE 流建立的筛选层 WDK Windows 筛选平台
- 内核模式标注驱动程序 WDK Windows 筛选平台
- 用户模式标注驱动程序 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 463cc5a3351a44626d4cf49a12680dc0cc89d882
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212549"
---
# <a name="callout-driver-programming-considerations"></a>标注驱动程序编程注意事项


编写 Windows 筛选平台标注驱动程序时，请考虑以下主题。

### <a name="user-mode-vs-kernel-mode"></a><a href="" id="user-mode-vs--kernel-mode"></a>用户模式与内核模式

如果可以使用 Windows 筛选平台中内置的标准筛选功能来执行所需的筛选，则 (Isv) 的独立软件供应商应该编写用户模式管理应用程序来配置筛选器引擎，而不是编写内核模式标注驱动程序。 仅当必须以标准内置筛选功能无法处理的方式处理网络数据时，才应编写内核模式标注驱动程序。 有关如何编写用户模式 Windows 筛选平台管理应用程序的信息，请参阅 Microsoft Windows SDK 中的 [Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220) 文档。

### <a name="choice-of-filtering-layer"></a>筛选层的选择

标注驱动程序应筛选网络堆栈中可能最高的筛选层上的网络数据。 例如，如果所需的筛选任务可在流层处理，则不应在网络层实现。 有关驱动程序应使用的筛选层的建议的详细信息，请参阅开发与 ipsec [兼容的标注驱动程序](developing-ipsec-compatible-callout-drivers.md)。

### <a name="blocking-at-the-application-layer-enforcement-ale-flow-established-layers"></a><a href="" id="blocking-at-the-application-layer-enforcement--ale--flow-established-l"></a>在应用程序层强制实施 (ALE) 流建立的层

通常情况下，如果已将某个标注添加到 ALE 流中的筛选器引擎，则在某个 *ALE 流建立* 的筛选层 (FWPM \_ 层 \_ ale \_ 流 \_ 建立 \_ 的 V4 或 FWPM \_ 层 \_ Ale \_ 流已 \_ 建立 \_ 的 V6) ，其 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数应绝不会返回 \_ 该操作的 .fwp 操作 \_ 块。 不应在某一 ALE 流建立的筛选层中对连接进行授权或拒绝决策。 此类决策应始终在其他一个 ALE 筛选层上进行。

此类 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数为操作返回 .Fwp 操作块的唯一有效原因是，如果 \_ 发生了 \_ 错误，当建立的连接未结束时，可能会造成潜在的安全风险。 在这种情况下， \_ 返回 \_ 操作的 .Fwp 操作块会关闭连接，以防止潜在安全风险被利用。

### <a name="callout-function-execution-time"></a>标注函数执行时间

由于筛选器引擎通常以 IRQL = 调度级别调用标注的标注函数 \_ ，因此请确保这些函数尽可能快地完成其执行，以使系统有效地运行。 位于 IRQL = 调度级别的扩展执行 \_ 会对系统的整体性能产生不利影响。

### <a name="injecting-into-the-receive-data-path"></a>注入接收数据路径

标注应在调用注入接收数据路径的 [数据包注入函数](packet-injection-functions.md) 之前重新计算 IP 校验和，因为在从 IP 数据包片段重新组合数据包时，原始数据包中的校验和可能不正确。 没有一种可靠的机制，用于指示网络缓冲区列表是否已从片段重新组合。

### <a name="inline-injection-of-tcp-packet-from-transport-layers"></a>传输层中 TCP 数据包的内联注入

由于 TCP 堆栈的锁定行为，因此传输层上的标注无法从 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) callout 函数插入新的或克隆的 TCP 数据包。 如果需要内联注入，则标注必须将 DPC 排入队列，才能执行注入。

### <a name="outgoing-ip-header-alignment"></a>传出 IP 标头对齐

描述网络缓冲区列表中的 IP 标头的 MDL ([**net buffer \_ \_ 当前 \_ MDL**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_current_mdl) ([**Net \_ buffer \_ list \_ FIRST \_ NB**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_first_nb) (*netBufferList*) # A4 # A5 在使用其中一种 [数据包注入函数](packet-injection-functions.md) 将数据包数据注入传出路径时，必须与指针对齐。 由于传入数据包的 IP 标头 MDL 可能是指针对齐的，因此，如果在将传入数据包注入到传出路径中时尚未对齐) ，标注必须重建 IP 标头 (。

## <a name="related-topics"></a>相关主题


[Windows 筛选平台标注驱动程序](windows-filtering-platform-callout-drivers2.md)

 

