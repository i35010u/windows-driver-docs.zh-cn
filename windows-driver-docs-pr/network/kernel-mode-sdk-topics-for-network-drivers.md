---
title: 网络驱动程序的内核模式 SDK 主题
description: 网络驱动程序的内核模式 SDK 主题
keywords:
- 用于网络驱动程序的内核模式 sdk 主题、内核模式 SDK 网络驱动程序、内核模式 Windows SDK 网络驱动程序、内核模式 Microsoft Windows SDK 网络驱动程序
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: e36fe621b3d63748648340db8bf6d76ddb97d437
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789729"
---
# <a name="kernel-mode-sdk-topics-for-network-drivers"></a>网络驱动程序的内核模式 SDK 主题

本部分列出了用于内核模式 Windows 网络驱动程序的头文件和主题。 本部分中的标头文件包含在 Windows 软件开发工具包 (SDK) ，而不是 Windows 驱动程序工具包 (WDK) ，因为它们也与用户模式网络应用程序共享。

> [!IMPORTANT]
> 本节的页眉主题包含用于定义、Oid、状态指示和其他不属于网络驱动程序引用的数据结构的页面。 参考主题包括结构、枚举、函数和回调。 
>
> 有关这些标头的网络驱动程序参考的详细信息，请参阅 [SDK 标头文件中的网络驱动程序参考](/previous-versions/windows/hardware/drivers/mt808525(v=vs.85))。

本部分包含：

* [Mstcpip.h](mstcpip-h.md)
* [Ntddndis.h](ntddndis-h.md)
* [Ws2def.h](ws2def-h.md)
