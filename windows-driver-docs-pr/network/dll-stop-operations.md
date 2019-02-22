---
title: DLL 停止操作
description: DLL 停止操作
ms.assetid: b49e9215-3781-4e19-8287-f484553ccb2e
keywords:
- IHV 扩展 DLL WDK 本机 802.11，停止操作
- 正在卸载 IHV 扩展 DLL
- 正在停止 IHV 扩展 DLL
- 本机 802.11 IHV 扩展 DLL WDK 停止操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c393f00942b2c4f33c755b74cb040c3cb453600a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543712"
---
# <a name="dll-stop-operations"></a>DLL 停止操作




 

操作系统停止并卸载 IHV 扩展 DLL 时。

-   托管的 dll 的最后一个无线 LAN (WLAN) 适配器在移除或禁用。

-   在主计算机关闭或重置。

操作系统按照以下顺序停止和卸载 IHV 扩展 DLL 时进行。

1.  操作系统首次调用[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452) IHV 处理程序函数为每个 WLAN 适配器由 IHV 扩展 DLL。 有关此操作的详细信息，请参阅[802.11 WLAN 适配器删除](802-11-wlan-adapter-removal.md)。

    在调用*Dot11ExtIhvDeinitAdapter*，IHV 扩展 DLL 不能调用任何 IHV 扩展函数与特定于适配器的操作，如相关[ **Dot11ExtNicSpecificExtension**](https://msdn.microsoft.com/library/windows/hardware/ff547526).

2.  然后，操作系统将调用[ *Dot11ExtIhvDeinitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547457) IHV 处理程序函数。 此函数时调用，IHV 扩展 DLL 必须释放所有已分配的资源并准备本身卸载。

    在调用*Dot11ExtIhvDeinitService*，IHV 扩展 DLL 不能调用任何 IHV 扩展函数。

3.  最后，操作系统将调用*DllMain*与 IHV 扩展 DLL 中的函数*fdwReason*参数设置为 DLL\_过程\_分离。 有关详细信息*DllMain*和 Dll，请参阅 Microsoft Windows SDK 文档中的主题"有关动态链接库中"。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://msdn.microsoft.com/library/windows/hardware/ff560609)。

 

 





