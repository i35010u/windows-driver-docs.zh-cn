---
title: 打开并初始化串行设备
description: 打开并初始化串行设备
ms.assetid: 08266561-4738-4313-b53b-d60081e875c7
keywords:
- 串行驱动程序 WDK，打开设备
- 串行驱动程序 WDK，设备初始化
- 串行设备 WDK，打开
- 串行设备 WDK，初始化
- 初始化串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba956fcf9980a655a9da970af1fd0bcdfcfca6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564230"
---
# <a name="opening-and-initializing-a-serial-device"></a>打开并初始化串行设备





当序列用作功能驱动程序时，以下注意事项适用于打开和初始化串行设备：

-   序列支持串行设备上一次只有一个打开。

-   打开时，设备是未定义的状态。 客户端应使用该设备之前初始化到已知状态的设备。 用户模式下客户端必须使用支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信功能。 内核模式下客户端可以使用[IOCTL\_串行\_设置\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547466)并[IOCTL\_串行\_内部\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547480)请求。

-   所有客户端必须打开串行设备时需要并通过它们是与端口后立即关闭设备。

-   Serenum 必须打开某个 RS-232 端口以枚举该端口。 RS-232 端口保持打开状态无限期的客户端不应使用 Serenum。

 

 




