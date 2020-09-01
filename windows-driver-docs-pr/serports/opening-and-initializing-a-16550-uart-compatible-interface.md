---
title: 打开并初始化 16550 UART 兼容接口
description: 打开并初始化 16550 UART 兼容接口
ms.assetid: 341cc1cb-bbcf-4514-8f5d-8970e49923c2
keywords:
- 串行驱动程序 WDK，16550 UART 兼容接口
- 通用异步接收器-发射器 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容的接口 WDK 串行设备
- 正在初始化 16550 UART 兼容的接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e7c6e8b179e14e748b69a2c1f3603ad7b1ab760
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186961"
---
# <a name="opening-and-initializing-a-16550-uart-compatible-interface"></a>打开并初始化 16550 UART 兼容接口

当串行用作较低级别的设备筛选器驱动程序时，以下注意事项适用于打开和初始化筛选器设备：

- 串行在筛选器设备上一次只能打开一个。

- 筛选器设备处于打开状态时处于未定义状态。

客户端在使用之前，应将筛选器设备初始化为已知状态。 用户模式客户端可以使用 IOCTL \_ 串行 \_ SET \_ Xxx 请求。 但请注意，与 Win32 兼容的应用程序必须使用 Microsoft Windows SDK 中 Windows 基础服务支持的通信函数。 内核模式客户端可以使用 IOCTL \_ 串行 \_ XXX 和 ioctl \_ 串行 \_ 内部 \_ Xxx 请求。 有关详细信息，请参阅 [ntddser](/windows-hardware/drivers/ddi/ntddser/) 标头。