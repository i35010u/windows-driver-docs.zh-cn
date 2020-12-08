---
title: DLL 停止操作
description: DLL 停止操作
keywords:
- IHV 扩展 DLL WDK 本机802.11，停止操作
- 卸载 IHV 扩展 DLL
- 正在停止 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK，停止操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ca65038b630a52e549e72de6d0e644e9d52baf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820107"
---
# <a name="dll-stop-operations"></a>DLL 停止操作




 

每次都将停止并卸载 IHV 扩展 DLL。

-   DLL 管理的上一个无线 LAN (WLAN) 适配器已被删除或禁用。

-   主机重置或关闭。

操作系统在停止并卸载 IHV 扩展 DLL 时遵循此顺序。

1.  操作系统首先为由 IHV 扩展 DLL 管理的每个 WLAN 适配器调用 [*Dot11ExtIhvDeinitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV 处理程序函数。 有关此操作的详细信息，请参阅 [802.11 WLAN 适配器的删除](802-11-wlan-adapter-removal.md)。

    调用 *Dot11ExtIhvDeinitAdapter* 后，IHV 扩展 DLL 不得调用与特定于适配器的操作相关的任何 IHV 扩展功能，如 [**Dot11ExtNicSpecificExtension**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)。

2.  然后，操作系统将调用 [*Dot11ExtIhvDeinitService*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV 处理程序函数。 如果调用此函数，则 IHV 扩展 DLL 必须释放所有已分配的资源，并为卸载做好准备。

    调用 *Dot11ExtIhvDeinitService* 之后，IHV 扩展 DLL 不得调用任何 IHV 扩展函数。

3.  最后，操作系统调用 IHV 扩展 DLL 中的 *DllMain* 函数，并将 *fdwReason* 参数设置为 DLL \_ 进程 \_ 分离。 有关 *DllMain* 和 dll 的详细信息，请参阅 Microsoft Windows SDK 文档中的主题 "关于 Dynamic-Link 库"。

有关 IHV 扩展性函数的详细信息，请参阅 [本机 802.11 IHV 扩展性函数](./native-802-11-ihv-extensibility-functions.md)。

 

 
