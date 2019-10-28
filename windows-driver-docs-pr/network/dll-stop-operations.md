---
title: DLL 停止操作
description: DLL 停止操作
ms.assetid: b49e9215-3781-4e19-8287-f484553ccb2e
keywords:
- IHV 扩展 DLL WDK 本机802.11，停止操作
- 卸载 IHV 扩展 DLL
- 正在停止 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，停止操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16f4a7cfe8eac2677b1f8573203047c38a2b0670
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838129"
---
# <a name="dll-stop-operations"></a>DLL 停止操作




 

每次都将停止并卸载 IHV 扩展 DLL。

-   DLL 管理的最后一个无线 LAN （WLAN）适配器已被删除或禁用。

-   主机重置或关闭。

操作系统在停止并卸载 IHV 扩展 DLL 时遵循此顺序。

1.  操作系统首先为由 IHV 扩展 DLL 管理的每个 WLAN 适配器调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV 处理程序函数。 有关此操作的详细信息，请参阅[802.11 WLAN 适配器的删除](802-11-wlan-adapter-removal.md)。

    调用*Dot11ExtIhvDeinitAdapter*后，IHV 扩展 DLL 不得调用与特定于适配器的操作相关的任何 IHV 扩展功能，如[**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)。

2.  然后，操作系统将调用[*Dot11ExtIhvDeinitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV 处理程序函数。 如果调用此函数，则 IHV 扩展 DLL 必须释放所有已分配的资源，并为卸载做好准备。

    调用*Dot11ExtIhvDeinitService*之后，IHV 扩展 DLL 不得调用任何 IHV 扩展函数。

3.  最后，操作系统将调用 IHV 扩展 DLL 中的*DllMain*函数，并将*fdwReason*参数设置为 DLL\_进程\_分离。 有关*DllMain*和 dll 的详细信息，请参阅 Microsoft Windows SDK 文档中的主题 "关于动态链接库"。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

 

 





