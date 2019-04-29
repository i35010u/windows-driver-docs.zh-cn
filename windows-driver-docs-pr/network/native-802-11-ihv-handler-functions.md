---
title: 本机 802.11 IHV 处理程序函数
description: 本部分介绍为本机 802.11 IHV 扩展 DLL 的本机 802.11 IHV 处理程序函数
keywords:
- 本机 802.11 IVH 处理程序函数
- 本机 802.11 IHV 扩展 DLL 处理程序函数
- WDK 本机 802.11 IVH 处理程序函数
ms.assetid: BF0DC1C7-48E1-487E-8F64-146BBA322F40
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c92d8407c06c5ab590d047f4378439f4c65c3a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368281"
---
# <a name="native-80211-ihv-handler-functions"></a>本机 802.11 IHV 处理程序函数

>[!IMPORTANT]
> [本机 802.11 无线 LAN](native-802-11-wireless-lan4.md)接口已弃用 Windows 10 及更高版本。 请改为使用 WLAN 设备驱动程序接口 (WDI)。 WDI 有关详细信息，请参阅[WLAN 通用 Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)。

本机 802.11 IHV 处理程序函数由 IHV 扩展 DLL 提供，并由操作系统执行以下调用：

- 分配和释放本机 802.11 框架中使用的缓冲区。
- 发送数据包，如定义的身份验证算法，通过 IHV 的无线 LAN (WLAN) 适配器的数据包。
- 接收数据包基于指定的 IEEE EtherType 值和隐私例外规则列表。
- IHV WLAN 适配器配置任何专有身份验证和密码算法的各种安全设置。
- IHV UI 扩展 DLL （如果已安装） 进程的事件通知的接口。 例如，IHV 扩展 DLL 可以通知 UI 扩展 DLL 中的基本服务集 (BSS) 网络连接所涉及的各种阶段。 

IHV UI 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV UI 扩展 DLL](native-802-11-ihv-ui-extensions-dll2.md)。

> [!NOTE]
> 除[Dot11ExtIhvGetVersionInfo](https://msdn.microsoft.com/library/windows/hardware/ff547464)并[Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470)，操作系统将调用通过函数指针成员与相关联的IHV处理程序函数[DOT11EXT_IHV_HANDLERS](https://msdn.microsoft.com/library/windows/hardware/ff547625)结构。 当操作系统将调用*Dot11ExtIhvInitService* IHV 处理程序函数，IHV 扩展 DLL 将返回到通过 IHV 处理程序函数的指针的列表*pDot11IHVHandlers*参数。

本部分介绍以下本机 802.11 IHV 处理程序函数。

- [Dot11ExtIhvAdapterReset](https://msdn.microsoft.com/library/windows/hardware/ff547434)
- [Dot11ExtIhvControl](https://msdn.microsoft.com/library/windows/hardware/ff547438)
- [Dot11ExtIhvCreateDiscoveryProfiles](https://msdn.microsoft.com/library/windows/hardware/ff547445)
- [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)
- [Dot11ExtIhvDeinitService](https://msdn.microsoft.com/library/windows/hardware/ff547457)
- [Dot11ExtIhvGetVersionInfo](https://msdn.microsoft.com/library/windows/hardware/ff547464)
- [Dot11ExtIhvInitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547469)
- [Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470)
- [Dot11ExtIhvInitVirtualStation](https://msdn.microsoft.com/library/windows/hardware/ff547475)
- [Dot11ExtIhvIsUIRequestPending](https://msdn.microsoft.com/library/windows/hardware/ff547479)
- [Dot11ExtIhvOneXIndicateResult](https://msdn.microsoft.com/library/windows/hardware/ff547482)
- [Dot11ExtIhvPerformCapabilityMatch](https://msdn.microsoft.com/library/windows/hardware/ff547488)
- [Dot11ExtIhvPerformPostAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547492)
- [Dot11ExtIhvPerformPreAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547499)
- [Dot11ExtIhvProcessSessionChange](https://msdn.microsoft.com/library/windows/hardware/ff547501)
- [Dot11ExtIhvProcessUIResponse](https://msdn.microsoft.com/library/windows/hardware/ff547504)
- [Dot11ExtIhvQueryUIRequest](https://msdn.microsoft.com/library/windows/hardware/ff547507)
- [Dot11ExtIhvReceiveIndication](https://msdn.microsoft.com/library/windows/hardware/ff547512)
- [Dot11ExtIhvReceivePacket](https://msdn.microsoft.com/library/windows/hardware/ff547513)
- [Dot11ExtIhvSendPacketCompletion](https://msdn.microsoft.com/library/windows/hardware/ff547516)
- [Dot11ExtIhvStopPostAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547521)
- [Dot11ExtIhvValidateProfile](https://msdn.microsoft.com/library/windows/hardware/ff547523)

