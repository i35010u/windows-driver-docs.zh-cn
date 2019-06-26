---
title: NDIS 版本概述
description: NDIS 版本概述
ms.assetid: 6ecd4040-2831-4238-8080-97edc6a7c3ba
keywords:
- 网络驱动程序 WDK、 NDIS 版本
- NDIS WDK，网络驱动程序中的版本
- 向后兼容性 WDK 网络
- 兼容性 WDK 网络
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: ed2f1c0546c4aa1186f152d87fdcab10a86d2733
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384378"
---
# <a name="overview-of-ndis-versions"></a>NDIS 版本概述

如果你正在编写多个版本的 Microsoft Windows 的 NDIS 驱动程序，请确保你使用的功能支持每个 Windows 版本上。 每个版本 NDIS 中添加新功能。 其他功能变得过时和更高版本的 NDIS 版本已删除。

这组设计指南文档针对的是 Windows Vista 和更高版本操作系统和 NDIS 6.0 和更高版本的驱动程序。 对于早期的 Windows 和 NDIS 版本的文档都包含在先前版本的文档。 有关 Windows XP 和 NDIS 5.1 文档，请参阅[Windows 2000 和 Windows XP 的网络设计指南](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565849(v=vs.85))。

> [!NOTE]
> 驱动程序可以通过调用查询的 NDIS 版本 [**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration) 函数与 *关键字* 参数设置为 **NdisVersion**. 

下表中描述 Windows 操作系统、 Microsoft Windows Driver Kit (WDK)，和驱动程序开发工具包 (DDK) 版本支持 NDIS 版本，以及对在 NDIS 版本之间的主要 NDIS 功能的支持。

| 操作系统 | 开发工具包 | 支持的 NDIS 版本 | CoNDIS | 反序列化的驱动程序 | 中间驱动程序 |
| --- | --- | --- | --- | --- | --- |
| Windows 95 | Windows NT 4.0 DDK 或 Windows 95 DDK | 3.1 |  |  |  |
|  |  | 添加了对微型端口驱动程序和插的支持。 |
| Windows 95 OSR2 | Windows NT 4.0 DDK 或 Windows 95 DDK | 4.0 |  |  |  |
|  |  | 协议驱动程序是一个 vxd 类型驱动程序。 |
| Windows 98 | Windows NT 4.0 DDK 或 Windows 98 DDK | 4.1 | X | X | X |
|  |  | 协议驱动程序是一个 vxd 类型驱动程序。 |
| Windows 98 SE | Windows NT 4.0 DDK 或 Windows 98 DDK | 5.0 | X | X | X |
|  |  | 添加了对电源管理和 WMI 支持。 |
| Windows Me | Windows NT 4.0 DDK 或 Windows 98 DDK 用于 Vxd | 5.0 | X | X | X |
| Windows NT 3.5 | Windows NT 3.5 DDK | 3.0 |  |  |  |
| Windows NT 4.0 | Windows NT 4.0 DDK | 4.0 |  |  |  |
|  |  | 添加这些功能： <ul><li>[**MiniportSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550524(v=vs.85))</li><li>[**ProtocolReceivePacket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff563251(v=vs.85))</li><li>[**MiniportAllocateComplete**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549352(v=vs.85))</li></ul> |
| Windows NT 4.0 SP3 | 使用更新后的 NDIS 标头和库的 Windows NT DDK | 4.1 | X | X | X |
| Windows 2000 | Windows 2000 DDK | 5.0 | X | X | X |
|  |  | 添加了对支持： <ul><li>与 Windows 95/98/我兼容新 INF 文件格式</li><li>即插即用和电源管理</li><li>WMI</li><li>LBFO</li><li>散播-聚集 DMA 支持反序列化的微型端口驱动程序</li></ul> |
| Windows XP | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721) | 5.1 | X | X | X |
|  |  | 添加了对支持： <ul><li>[**MiniportCancelSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549359(v=vs.85))</li><li>[**MiniportPnPEventNotify**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550487(v=vs.85))</li><li>[**MiniportShutdown**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550533(v=vs.85))</li><li>[**NdisCancelSendPackets**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff550821(v=vs.85))</li><li>[**NdisCopyFromPacketToPacketSafe**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551071(v=vs.85))</li><li>[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgeneratepartialcancelid)</li><li>[**NdisGetFirstBufferFromPacketSafe**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552066(v=vs.85))</li><li>[**NdisGetPoolFromPacket**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552090(v=vs.85))</li><li>[**NdisGetSharedDataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetshareddataalignment)</li><li>[**NdisIMGetCurrentPacketStack**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552155(v=vs.85))</li><li>[**NdisIMNotifyPnPEvent**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552203(v=vs.85))</li><li>[**NdisQueryPendingIOCount**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff554456(v=vs.85))</li><li>[**NDIS\_获取\_数据包\_取消\_ID**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556988(v=vs.85))</li><li>[**NDIS\_设置\_数据包\_取消\_ID**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557195(v=vs.85))</li><li>[OID\_GEN\_MACHINE\_NAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-machine-name)</li><li>新的微型端口驱动程序特性标志</li><li>64 位的统计计数器</li><li>远程 NDIS</li><li>散播-聚集支持序列化和反序列化微型端口驱动程序</li><li>堆叠的中间驱动程序的数据包</li><li>VLAN 标记</li><li>卸载 UDP 封装 ESP 数据包 (仅 Windows Server 2003) 的处理</li><li>Wi-fi 保护访问 (WPA) 在 Windows XP SP1</li></ul> |
|  |  | 已删除的支持： <ul><li>完整 Mac 驱动程序</li><li>NDIS 3.0 协议</li><li>**NdisQueryMapRegisterCount**</li><li>EISA 总线</li></ul> |
| Windows Vista | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721) | 6.0 | X | X | X |
|  |  | 以下重大改进客户端和服务器提供显著的性能提升： <ul><li>网络数据打包</li><li>发送和接收路径</li><li>运行时重新配置功能</li><li>散播-聚集 DMA</li><li>筛选器驱动程序</li><li>接收到的数据处理的多处理器缩放</li><li>卸载到 Nic 的 TCP 任务</li></ul> |
|  |  | 以下改进简化驱动程序开发： <ul><li>简化驱动程序初始化</li><li>NDIS 接口的版本控制支持</li><li>简化重置处理</li><li>标准接口，用于获取管理信息</li><li>要将筛选器中间驱动程序的筛选器驱动程序模型</li></ul> |
|  |  | 有关 NDIS 6.0 功能的详细信息，请参阅[简介 NDIS 6.0](introduction-to-ndis-6-0.md)。 |
|  |  | 向后兼容性和不支持在 NDIS 6.0 驱动程序中的过时功能有关的信息，请参阅[NDIS 6.0 向后兼容性](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)。 |
| Windows Vista Service pack 1 (SP1) 和 Windows Server 2008 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.1 | X | X | X |
|  |  | NDIS 6.1 功能有关的信息，请参阅[简介 NDIS 6.1](introduction-to-ndis-6-1.md)。 |
| Windows 7 和 Windows Server 2008 R2 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.20 | X | X | X |
|  |  | NDIS 6.20 功能有关的信息，请参阅[简介 NDIS 6.20](introduction-to-ndis-6-20.md)。 |
|  |  | 向后兼容性和不支持在 NDIS 6.20 驱动程序中的过时功能有关的信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。 |
| Windows 8 和 Windows Server 2012 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.30 | X | X | X |
|  |  | NDIS 6.30 功能有关的信息，请参阅[简介 NDIS 6.30](introduction-to-ndis-6-30.md)。 |
| Windows 8.1 和 Windows Server 2012 R2 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.40 | X | X | X |
|  |  | NDIS 6.40 功能有关的信息，请参阅[简介 NDIS 6.40](introduction-to-ndis-6-40.md)。 |
| Windows 10 版本 1507 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.50 | X | X | X |
|   |   | 有关 NDIS 6.50 功能的详细信息，请参阅[简介 NDIS 6.50](introduction-to-ndis-6-50.md)。 | 
| Windows 10 版本 1511 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.51 | X | X | X |
| Windows 10，版本 1607年和 Windows Server 2016 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.60 | X | X | X |
|   |   | 有关 NDIS 6.60 功能的详细信息，请参阅[简介 NDIS 6.60](introduction-to-ndis-6-60.md)。 | 
| Windows 10 版本 1703 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.70 | X | X | X |
|   |   | NDIS 6.70 正好与网络适配器 WDF 类扩展的预览版本也称为 [NetAdapterCx](../netcx/index.md)。<p>有关 NDIS 6.70 功能的详细信息，请参阅[简介 NDIS 6.70](introduction-to-ndis-6-70.md)。</p> |
| Windows 10 版本 1709 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.80 | X | X | X |
|   |   | 有关 NDIS 6.80 功能的详细信息，请参阅[简介 NDIS 6.80](introduction-to-ndis-6-80.md)。 | 
| Windows 10 版本 1803 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.81 | X | X | X |
|   |   | 有关 NDIS 6.81 功能的详细信息，请参阅[简介 NDIS 6.81](introduction-to-ndis-6-81.md)。 |
| Windows 10 版本 1809 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.82 | X | X | X |
|   |   | 有关 NDIS 6.82 功能的详细信息，请参阅[简介 NDIS 6.82](introduction-to-ndis-6-82.md)。 |
| Windows 10 版本 1903 | 请参阅[下载 Windows 硬件开发工具包](https://go.microsoft.com/fwlink/p/?linkid=239721)。 | 6.83 | X | X | X |
|   |   | 有关 NDIS 6.83 功能的详细信息，请参阅[简介 NDIS 6.83](introduction-to-ndis-6-83.md)。 |
