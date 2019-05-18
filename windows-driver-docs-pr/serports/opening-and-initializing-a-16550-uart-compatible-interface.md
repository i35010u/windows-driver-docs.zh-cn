---
title: 打开并初始化 16550 UART 兼容接口
description: 打开并初始化 16550 UART 兼容接口
ms.assetid: 341cc1cb-bbcf-4514-8f5d-8970e49923c2
keywords:
- 串行驱动程序 WDK，16550 UART 兼容接口
- 通用的异步接收方发射机 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容接口 WDK 串行设备
- 初始化 16550 UART 兼容接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a44551f7aacb7893ef72480377cf31ae84b9ff
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836356"
---
# <a name="opening-and-initializing-a-16550-uart-compatible-interface"></a>打开并初始化 16550 UART 兼容接口

当序列用作较低级别设备筛选器驱动程序时，以下注意事项适用于打开和初始化筛选器设备：

- 序列支持筛选器设备上一次只有一个打开。

- 打开时，筛选器设备是未定义的状态。

客户端应使用它之前，初始化筛选器设备连接到已知状态。 用户模式下客户端可以使用 IOCTL\_串行\_设置\_Xxx 请求。 但请注意，与 Win32 兼容应用程序必须使用支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信函数。 内核模式下客户端可以使用 IOCTL\_串行\_Xxx 和 IOCTL\_串行\_内部\_Xxx 请求。 有关详细信息请参阅[ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)标头。
