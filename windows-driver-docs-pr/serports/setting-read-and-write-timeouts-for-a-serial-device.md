---
title: 设置串行设备的读取和写入超时
description: 设置串行设备的读取和写入超时
ms.assetid: ed5b80a9-93cb-4e3f-9038-e715be35f206
keywords:
- 串行驱动程序 WDK，超时
- 超时 WDK 串行设备
- 串行设备 WDK，超时
- 读取超时的 WDK 串行设备
- 写入超时的 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d7990770ae3ed4134bf26c1b92830bdaac1a32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845388"
---
# <a name="setting-read-and-write-timeouts-for-a-serial-device"></a>设置串行设备的读取和写入超时

客户端可以使用[**IOCTL\_串行\_集\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)请求设置系统提供的 SERIAL 驱动程序用于读取和写入请求的超时值。 在传输请求的字节数或发生超时事件之前，Serial 会继续传输字节。

Serial 中的超时操作符合 Microsoft Windows SDK 中 Windows 基础服务支持的通信功能所支持的[COM 端口](configuration-of-com-ports.md)的用户模式操作。 "。

请注意，超时操作在排队时不会应用于挂起的请求。 超时操作在请求成为最新（即，sys.databases 开始处理请求）之后应用到请求。

有关读取和写入超时的详细信息，请参阅以下内容：

- Windows 驱动程序工具包（WDK）中 Ntddser 标头文件中的[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)结构。

- Windows SDK 中的 Windows 基础服务支持的[**SetCommTimeouts**](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setcommtimeouts)函数和[**COMMTIMEOUTS**](https://docs.microsoft.com/windows/desktop/api/winbase/ns-winbase-_commtimeouts)结构。
