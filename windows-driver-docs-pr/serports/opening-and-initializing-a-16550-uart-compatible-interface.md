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
ms.openlocfilehash: 32eae1924f7f04fad3220ed2f7b03722a9f97628
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862830"
---
# <a name="opening-and-initializing-a-16550-uart-compatible-interface"></a>打开并初始化 16550 UART 兼容接口

当串行用作较低级别的设备筛选器驱动程序时，以下注意事项适用于打开和初始化筛选器设备：

- 串行在筛选器设备上一次只能打开一个。

- 筛选器设备处于打开状态时处于未定义状态。

客户端在使用之前，应将筛选器设备初始化为已知状态。 用户模式客户端可以使用\_串行\_设置\_Xxx 请求的 IOCTL。 但请注意，与 Win32 兼容的应用程序必须使用 Microsoft Windows SDK 中 Windows 基础服务支持的通信函数。 内核模式客户端可以使用 IOCTL\_串行\_Xxx 和 IOCTL\_串行\_内部\_Xxx 请求。 有关详细信息，请参阅[ntddser](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)标头。
