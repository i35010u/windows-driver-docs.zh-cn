---
title: 打开并初始化串行设备
description: 打开并初始化串行设备
ms.assetid: 08266561-4738-4313-b53b-d60081e875c7
keywords:
- 串行驱动程序 WDK，设备打开
- 串行驱动程序 WDK，设备初始化
- 串行设备 WDK，打开
- 串行设备 WDK，初始化
- 正在初始化串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af94445882c9c32d0c9479ce536d3289e0df4f97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842440"
---
# <a name="opening-and-initializing-a-serial-device"></a>打开并初始化串行设备

当串行用作函数驱动程序时，以下注意事项适用于打开和初始化串行设备：

- 串行设备上一次只支持一个打开的串行设备。

- 设备在打开时处于未定义状态。 在使用设备之前，客户端应将设备初始化为已知状态。 用户模式客户端必须使用 Microsoft Windows SDK 中 Windows 基础服务支持的通信功能。 内核模式客户端可以使用 IOCTL\_串行\_集\_Xxx 和 IOCTL\_串行\_内部\_Xxx 请求。 有关详细信息，请参阅[ntddser](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddser/)标头。

- 所有客户端都必须在需要时打开串行设备，并通过端口立即关闭设备。

- Serenum 必须打开 RS-232 端口来枚举端口。 如果客户端保持打开的 RS-232 端口，则不应使用 Serenum。
