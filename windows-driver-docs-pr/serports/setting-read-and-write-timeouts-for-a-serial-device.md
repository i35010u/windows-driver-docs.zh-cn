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
ms.openlocfilehash: 4a93ddf03f7565b92d41abede01287646743d2bf
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715866"
---
# <a name="setting-read-and-write-timeouts-for-a-serial-device"></a>设置串行设备的读取和写入超时

客户端可以使用 [**IOCTL \_ 串行 \_ 设置 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts) 请求设置系统提供的 Serial.sys 驱动程序用于读取和写入请求的超时值。 Serial.sys 继续传输字节，直到传输请求的字节数或发生超时事件为止。

Serial.sys 中的超时操作符合 Microsoft Windows SDK 中 Windows 基础服务支持的通信功能所支持的 [COM 端口](configuration-of-com-ports.md) 的用户模式操作的情况。

请注意，超时操作在排队时不会应用于挂起的请求。 超时操作在请求变为当前 (后应用于请求，即 Serial.sys 开始处理请求) 。

有关读取和写入超时的详细信息，请参阅以下内容：

- Windows 驱动程序工具包 (WDK) 中的 Ntddser 标头文件中的 [**序列 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts) 结构。

- Windows SDK 中的 Windows 基础服务支持的 [**SetCommTimeouts**](/windows/win32/api/winbase/nf-winbase-setcommtimeouts) 函数和 [**COMMTIMEOUTS**](/windows/win32/api/winbase/ns-winbase-_commtimeouts) 结构。