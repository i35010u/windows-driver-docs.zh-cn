---
title: NDIS 版本概述
description: NDIS 版本概述
keywords:
- 网络驱动程序 WDK，NDIS 版本
- NDIS WDK，网络驱动程序中的版本
- 向后兼容性 WDK 网络
- 兼容性 WDK 网络
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 853d8874162d6f5495805cf7c31b46d012717c17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801339"
---
# <a name="overview-of-ndis-versions"></a>NDIS 版本概述

如果要为多个 Microsoft Windows 版本编写 NDIS 驱动程序，请确保每个 Windows 版本都支持你正在使用的功能。 每个版本都已将新功能添加到 NDIS。 其他功能已过时，并已从以后的 NDIS 版本中删除。

这一组设计指南文档面向 Windows Vista 及更高版本的操作系统以及 NDIS 6.0 和更高版本的驱动程序。 以前版本的文档中包含早期版本 Windows 和 NDIS 版本的文档。 有关 Windows XP 和 NDIS 5.1 文档，请参阅 [windows 2000 和 WINDOWS XP 网络设计指南](/previous-versions/windows/hardware/network/ff565849(v=vs.85))。

> [!NOTE]
> 驱动程序可以通过调用 [**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration) 函数来查询 NDIS 版本，并将 *关键字* 参数设置为 **NdisVersion**。 

下表介绍了 Windows 操作系统、Microsoft Windows 驱动程序工具包 (WDK) 和驱动程序开发工具包 (DDK) 版本支持 NDIS 版本，并支持跨 NDIS 版本的主要 NDIS 功能。

| 操作系统 | 开发工具包 | 支持的 NDIS 版本 | CoNDIS | 反序列化驱动程序 | 中间驱动程序 |
| --- | --- | --- | --- | --- | --- |
| Windows 95 | Windows NT 4.0 DDK 或 Windows 95 DDK | 3.1 |  |  |  |
|  |  | 添加了对微型端口驱动程序和即插即用的支持。 |
| Windows 95 OSR2 | Windows NT 4.0 DDK 或 Windows 95 DDK | 4.0 |  |  |  |
|  |  | 协议驱动程序是一个 vxd 类型的驱动程序。 |
| Windows 98 | Windows NT 4.0 DDK 或 Windows 98 DDK | 4.1 | X | X | X |
|  |  | 协议驱动程序是一个 vxd 类型的驱动程序。 |
| Windows 98 SE | Windows NT 4.0 DDK 或 Windows 98 DDK | 5.0 | X | X | X |
|  |  | 添加了对电源管理和 WMI 的支持。 |
| Windows Me | 用于 Vxd 的 windows NT 4.0 DDK 或 Windows 98 DDK | 5.0 | X | X | X |
| Windows NT 3。5 | Windows NT 3.5 DDK | 3.0 |  |  |  |
| Windows NT 4.0 | Windows NT 4.0 DDK | 4.0 |  |  |  |
|  |  | 添加了以下功能： <ul><li>[**MiniportSendPackets**](/previous-versions/windows/hardware/network/ff550524(v=vs.85))</li><li>[**ProtocolReceivePacket**](/previous-versions/windows/hardware/network/ff563251(v=vs.85))</li><li>[**MiniportAllocateComplete**](/previous-versions/windows/hardware/network/ff549352(v=vs.85))</li></ul> |
| Windows NT 4.0 SP3 | 带有更新的 NDIS 标头和库的 Windows NT DDK | 4.1 | X | X | X |
| Windows 2000 | Windows 2000 DDK | 5.0 | X | X | X |
|  |  | 添加了对的支持： <ul><li>与 Windows 95/98/Me 兼容的新 INF 文件格式</li><li>即插即用和电源管理</li><li>WMI</li><li>LBFO</li><li>散播/聚集 DMA 对反端口反序列化驱动程序的支持</li></ul> |
| Windows XP | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721) | 5.1 | X | X | X |
|  |  | 添加了对的支持： <ul><li>[**MiniportCancelSendPackets**](/previous-versions/windows/hardware/network/ff549359(v=vs.85))</li><li>[**MiniportPnPEventNotify**](/previous-versions/windows/hardware/network/ff550487(v=vs.85))</li><li>[**MiniportShutdown**](/previous-versions/windows/hardware/network/ff550533(v=vs.85))</li><li>[**NdisCancelSendPackets**](/previous-versions/windows/hardware/network/ff550821(v=vs.85))</li><li>[**NdisCopyFromPacketToPacketSafe**](/previous-versions/windows/hardware/network/ff551071(v=vs.85))</li><li>[**NdisGeneratePartialCancelId**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)</li><li>[**NdisGetFirstBufferFromPacketSafe**](/previous-versions/windows/hardware/network/ff552066(v=vs.85))</li><li>[**NdisGetPoolFromPacket**](/previous-versions/windows/hardware/network/ff552090(v=vs.85))</li><li>[**NdisGetSharedDataAlignment**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)</li><li>[**NdisIMGetCurrentPacketStack**](/previous-versions/windows/hardware/network/ff552155(v=vs.85))</li><li>[**NdisIMNotifyPnPEvent**](/previous-versions/windows/hardware/network/ff552203(v=vs.85))</li><li>[**NdisQueryPendingIOCount**](/previous-versions/windows/hardware/network/ff554456(v=vs.85))</li><li>[**NDIS \_ 获取 \_ 数据包 \_ 取消 \_ ID**](/previous-versions/windows/hardware/network/ff556988(v=vs.85))</li><li>[**NDIS \_ 设置 \_ 数据包 \_ 取消 \_ ID**](/previous-versions/windows/hardware/network/ff557195(v=vs.85))</li><li>[OID \_ 生成 \_ 计算机 \_ 名称](./oid-gen-machine-name.md)</li><li>新的微型端口驱动程序特性标志</li><li>64位统计计数器</li><li>远程 NDIS</li><li>散点/集合支持序列化和反序列化微型端口驱动程序</li><li>用于中间驱动程序的数据包堆栈</li><li>VLAN 标记</li><li>仅在 Windows Server 2003 (上卸载 UDP-Encapsulated ESP 数据包的处理) </li><li>Windows XP SP1 中的 Wi-Fi 保护访问 (WPA) </li></ul> |
|  |  | 丢弃了对以下内容的支持： <ul><li>完整的 Mac 驱动程序</li><li>NDIS 3.0 协议</li><li>**NdisQueryMapRegisterCount**</li><li>EISA 总线</li></ul> |
| Windows Vista | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721) | 6.0 | X | X | X |
|  |  | 下面的重大改进为客户端和服务器提供了显著的性能提升： <ul><li>网络数据打包</li><li>发送和接收路径</li><li>运行时重新配置功能</li><li>散点/集合 DMA</li><li>筛选器驱动程序</li><li>接收的数据处理的多处理器缩放</li><li>将 TCP 任务卸载到 Nic</li></ul> |
|  |  | 以下改进简化了驱动程序的开发： <ul><li>简化的驱动程序初始化</li><li>对 NDIS 接口的版本控制支持</li><li>简化的重置处理</li><li>用于获取管理信息的标准接口</li><li>用于替换筛选器中间驱动程序的筛选器驱动程序模型</li></ul> |
|  |  | 有关 NDIS 6.0 功能的详细信息，请参阅 [ndis 6.0 简介](introduction-to-ndis-6-0.md)。 |
|  |  | 有关 NDIS 6.0 驱动程序不支持的向后兼容性和过时功能的信息，请参阅 [ndis 6.0 向后兼容性](/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)。 |
| Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.1 | X | X | X |
|  |  | 有关 NDIS 6.1 功能的信息，请参阅 [ndis 6.1 简介](introduction-to-ndis-6-1.md)。 |
| Windows 7 和 Windows Server 2008 R2 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.20 | X | X | X |
|  |  | 有关 NDIS 6.20 功能的信息，请参阅 [ndis 6.20 简介](introduction-to-ndis-6-20.md)。 |
|  |  | 有关 NDIS 6.20 驱动程序不支持的向后兼容性和过时功能的信息，请参阅 [ndis 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。 |
| Windows 8 和 Windows Server 2012 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.30 | X | X | X |
|  |  | 有关 NDIS 6.30 功能的信息，请参阅 [ndis 6.30 简介](introduction-to-ndis-6-30.md)。 |
| Windows 8.1 和 Windows Server 2012 R2 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.40 | X | X | X |
|  |  | 有关 NDIS 6.40 功能的信息，请参阅 [ndis 6.40 简介](introduction-to-ndis-6-40.md)。 |
| Windows 10 版本1507 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.50 | X | X | X |
|   |   | 有关 NDIS 6.50 功能的详细信息，请参阅 [ndis 6.50 简介](introduction-to-ndis-6-50.md)。 | 
| Windows 10 版本 1511 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.51 | X | X | X |
| Windows 10 版本1607和 Windows Server 2016 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.60 | X | X | X |
|   |   | 有关 NDIS 6.60 功能的详细信息，请参阅 [ndis 6.60 简介](introduction-to-ndis-6-60.md)。 | 
| Windows 10 版本 1703 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.70 | X | X | X |
|   |   | 带有网络适配器 WDF 类扩展的预览版本的 NDIS 6.70 coincided，也称为 [NetAdapterCx](../netcx/index.md)。<p>有关 NDIS 6.70 功能的详细信息，请参阅 [ndis 6.70 简介](introduction-to-ndis-6-70.md)。</p> |
| Windows 10 版本 1709 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.80 | X | X | X |
|   |   | 有关 NDIS 6.80 功能的详细信息，请参阅 [ndis 6.80 简介](introduction-to-ndis-6-80.md)。 | 
| Windows 10 版本 1803 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.81 | X | X | X |
|   |   | 有关 NDIS 6.81 功能的详细信息，请参阅 [ndis 6.81 简介](introduction-to-ndis-6-81.md)。 |
| Windows 10 版本 1809 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.82 | X | X | X |
|   |   | 有关 NDIS 6.82 功能的详细信息，请参阅 [ndis 6.82 简介](introduction-to-ndis-6-82.md)。 |
| Windows 10 版本 1903 | 请参阅 [适用于 Windows 硬件开发的下载工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.83 | X | X | X |
|   |   | 有关 NDIS 6.83 功能的详细信息，请参阅 [ndis 6.83 简介](introduction-to-ndis-6-83.md)。 |
