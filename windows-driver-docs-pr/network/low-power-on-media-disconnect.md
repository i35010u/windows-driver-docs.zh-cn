---
title: 在媒体断开连接的低能耗
description: 在媒体断开连接的低能耗
ms.assetid: 592f3835-47ec-443a-9ab5-e700fed2f7f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef84631c6abb275ddf4fe325c3d00324fffa533
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523226"
---
# <a name="low-power-on-media-disconnect"></a>在媒体断开连接的低能耗





在媒体断开连接低能耗 (D3 上的断开连接) 功能通过将网络适配器放置在低功耗状态 (D3) 媒体已断开连接时节省电能。 当媒体重新连接时，网络适配器被还原到全功率状态 (D0)。

NDIS 使用 D3 上的断开连接在这些情况下的功能：

-   网络适配器硬件必须都能够生成媒体上的唤醒事件连接。

-   微型端口驱动程序必须报告中的网络适配器的唤醒事件功能**MinLinkChangeWakeUp**的成员[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

-   值**MinLinkChangeWakeUp**必须与对应的值**DeviceWake**的成员[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，它由报告[ **IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664) IRP。

-   微型端口驱动程序必须注册为 NDIS 6.20 驱动程序或更高版本。

-   网络适配器必须是以太网 PCI 适配器。

-   唤醒事件功能必须通过启用 **\*DeviceSleepOnDisconnect**标准 INF 文件关键字。

-   必须能够正确传播发生唤醒事件时提供完全支持在计算机的计算机芯片集确定。 NDIS 验证这通过查询 DEVPKEY\_PciDevice\_S0WakeupSupported PCI 属性。

在计算机完全供电处于工作状态 (S0) 时，请注意，D3 上的断开的连接才可用。 当计算机进入睡眠状态，以防止计算机时从外部循环的链接状态; 唤醒时取消此功能它是一个开关打开时关闭和打开。 有关设置的详细信息低功耗状态，当计算机进入睡眠状态，请参阅[低的电源可用于 LAN 唤醒](low-power-for-wake-on-lan.md)。

微型端口驱动程序报表 D3 上的在初始化期间断开连接的功能。 详细了解 reporting D3 断开连接时功能，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

 **\*DeviceSleepOnDisconnect**标准 INF 文件关键字指定设备已启用还是禁用对 D3 的支持上断开连接。 有关此 INF 关键字的详细信息，请参阅[电源管理的标准化 INF 关键字](standardized-inf-keywords-for-power-management.md)。

在初始化期间，支持 D3 上的断开的连接必须报告其中它可以支持的功能，以通知媒体的操作系统最低功率级别微型端口驱动程序连接事件。 微型端口驱动程序报告中的电源级别**MinLinkChangeWakeUp**的成员[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。 例如，微型端口驱动程序可以报告**NdisDeviceStateD3**。

下图说明了要网络适配器设置为低功耗状态后一个介质断开连接事件, 的事件的顺序。

![说明要 nic 设置为低功耗状态后一个介质断开连接事件, 的事件序列关系图](images/d3ondisconnect.png)

当适配器检测到媒体断开连接时，将发生以下序列：

1.  网络适配器硬件检测媒体断开连接事件，并将信息传递给微型端口驱动程序。

2.  NDIS 媒体断开连接事件使用微型端口驱动程序通知[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含[ **NDIS\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh205390)结构。 MediaConnectStateDisconnected 值中设置**MediaConnectState**的成员**NDIS\_链接\_状态**结构。

3.  使用 NDIS [OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)若要禁用 LAN 唤醒，并启用唤醒媒体连接 (NDIS\_PM\_唤醒\_ON\_链接\_更改\_中设置已启用**WakeUpFlags**成员)。

4.  使用 NDIS [OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780) OID 以通知新的电源状态 (D3) 的微型端口驱动程序。

5.  NDIS 发送 PCIe 总线[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766) IRP 等待重新连接事件。

6.  NDIS 到 D3 状态设置 PCIe 总线[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744) IRP。

下图说明了要还原到的网络适配器的全部功能之后媒体连接事件, 的事件的顺序。

![说明要还原到 nic 的完整功能之后媒体连接事件, 的事件序列关系图](images/d0onconnect.png)

在媒体重新连接时将发生以下序列：

1.  网络适配器中唤醒系统通过断言唤醒\#PCIe 总线或 PME 上\#PCI 总线上。

2.  总线完成挂起[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766) IRP。 IRP 正在等待完成从断开连接序列中的最后一个步骤。

3.  NDIS 具有设置到全功率 (D0) 总线[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744) IRP。

4.  NDIS 通知微型端口驱动程序，在具有 OID 的全部功能 (D0) 状态的网络适配器设置的请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)。

5.  网络适配器通知 NDIS 媒体连接具有事件[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示。 **MediaConnectStateConnected**中设置值**MediaConnectState**的成员[ **NDIS\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh205390)结构。

如果微型端口驱动程序支持从 NDIS 6.30 [ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示，它必须发出这如果网络适配器中唤醒系统的状态通知。 此状态通知时处理 OID 设置驱动程序问题的请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)全功率 (D0) 状态转换。

有关详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

**请注意**  如果微型端口驱动程序将发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示它必须执行此操作才能发出[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)状态指示。

 

 

 





