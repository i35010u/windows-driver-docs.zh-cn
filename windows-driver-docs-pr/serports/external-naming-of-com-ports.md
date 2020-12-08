---
title: COM 端口的外部命名
description: COM 端口的外部命名
keywords:
- 串行驱动程序 WDK，COM 端口
- COM 端口 WDK 串行设备
- 串行设备 WDK，COM 端口
- 为串行设备命名 WDL
- 外部命名 WDK 串行设备
- 符号链接 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa6150168cb7713691a929ec1434568ce2884de8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812033"
---
# <a name="external-naming-of-com-ports"></a>COM 端口的外部命名





默认情况下，串行函数驱动程序会为串行端口创建符号链接名称，并 \_ \_ 为该端口注册 GUID DEVINTERFACE COMPORT *设备接口* 。 按照定义，串行端口只有在具有与其关联的 COM 端口设备接口的情况下才是 [com 端口](configuration-of-com-ports.md) 。

对于即插即用串行设备，外部命名由设备硬件密钥下的 **SerialSkipExternalNaming** 条目值控制。 如果 **SerialSkipExternalNaming** 条目值不存在，或其值为零，则串行创建一个 COM 端口设备接口;否则，串行不会创建 COM 端口接口。 串行不支持旧 COM 端口的此项值，并且始终为旧 COM 端口创建 COM 端口设备接口。

串行执行以下任务来创建 COM 端口设备接口：

- 在 **\\ DosDevices \\** &lt; *portvalue* &gt; 与 COM 端口的内部设备对象名称之间创建符号链接。

  &lt;*Portvalue* &gt;COM 端口的 **portvalue** (值或 **标识符**) 条目值。 端口类安装程序将 **portvalue** 设置为 com <em> &lt; n &gt;</em>，其中 &lt; *&gt; n* 是安装程序从 [com 端口数据库](com-port-database.md)获取的 com 端口号。 串行使用此名称创建端口的符号链接。 对 Windows 支持的 COM 端口数量没有限制。 用户模式客户端使用符号链接名称打开 COM 端口。

- 在 **\\ 注册表 \\ 计算机 \\ 硬件 \\ DeviceMap \\ SERIALCOMM** 项下写入一个条目值。

  条目值的名称是 **\\ 设备 \\ 序列** &lt; *m &gt; ，* 其中 *&lt; m &gt;* 是通过串行分配给设备的数字。 请注意，串行设备号 *&lt; m &gt;* 不同于 COM 端口号 *&lt; n &gt;*。 **\\ 设备 \\ 序列** m 的值 &lt; *m* &gt; 设置为 **portvalue** 的值。

- \_为 COM 端口注册类型为 GUID DEVINTERFACE COMPORT 的设备接口 \_ 。

  客户端可以注册 COM 端口接口到达的通知，或者可以获取所有已注册 COM 端口接口的符号链接名称。

有关串行如何使用注册表项值的详细信息，请参阅 [serial 的注册表设置](registry-settings-for-serial.md)。

 

 




