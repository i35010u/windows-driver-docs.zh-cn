---
title: 设置串行设备的读取和写入超时
description: 设置串行设备的读取和写入超时
ms.assetid: ed5b80a9-93cb-4e3f-9038-e715be35f206
keywords:
- 串行驱动程序 WDK，超时值
- 超时 WDK 串行设备
- 串行设备 WDK，超时值
- 读取 WDK 串行设备的超时值
- 写入 WDK 串行设备的超时值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7576f6bda821226044325bd87028643a413f907c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562598"
---
# <a name="setting-read-and-write-timeouts-for-a-serial-device"></a>设置串行设备的读取和写入超时





可以使用客户端[ **IOCTL\_串行\_设置\_超时**](https://msdn.microsoft.com/library/windows/hardware/ff546772)设置超时值的系统提供 Serial.sys 驱动程序用于读取和写入请求请求数。 Serial.sys 继续传输字节，直到传输请求的字节数或发生超时事件。

Serial.sys 中的超时操作是符合的用户模式下操作[COM 端口](configuration-of-com-ports.md)受支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信函数。

请注意已排队时，超时操作不应用对挂起的请求。 超时操作应用到请求，请求将成为当前后 （即，Serial.sys 开始处理请求）。

有关读取和写入超时的详细信息，请参阅：

-   [**串行\_超时**](https://msdn.microsoft.com/library/windows/hardware/hh439614) Ntddser.h 标头文件中 Windows Driver Kit (WDK) 中的结构。

-   [ **SetCommTimeouts** ](https://msdn.microsoft.com/library/windows/desktop/aa363437)函数和[ **COMMTIMEOUTS** ](https://msdn.microsoft.com/library/windows/desktop/aa363190) Windows 基本服务支持的结构Windows SDK。

 

 




