---
title: COM 端口的外部命名
description: COM 端口的外部命名
ms.assetid: d517bc73-9687-45f8-a5f8-837ffe868fae
keywords:
- 串行驱动程序 WDK、 COM 端口
- COM 端口 WDK 串行设备
- 串行设备 WDK、 COM 端口
- 名称 WDL 串行设备
- 外部命名 WDK 设备
- 符号链接 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e55032761d413e3d12eb4d5ab5c0cb4c99023189
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380007"
---
# <a name="external-naming-of-com-ports"></a>COM 端口的外部命名





默认情况下，串行函数驱动程序创建串行端口的符号链接名称，并注册一个 GUID\_DEVINTERFACE\_COMPORT*设备接口*端口。 根据定义，是串行端口[COM 端口](configuration-of-com-ports.md)仅当它具有与之关联的 COM 端口设备接口。

对于插串行设备，在由控制外部命名**SerialSkipExternalNaming**条目下设备的硬件密钥的值。 如果**SerialSkipExternalNaming**条目值不存在，或其值为 0，序列会创建一个 COM 端口设备接口; 否则为序列不会创建一个 COM 端口接口。 序列不支持此项值的传统的 COM 端口，并始终创建传统的 COM 端口的 COM 端口设备接口。

序列将执行以下任务来创建一个 COM 端口设备接口：

- 创建符号链接之间 **\\DosDevices\\**&lt;*PortName* &gt;和 COM 端口的内部设备对象名称。

  &lt;*PortName* &gt;的值**PortName** (或**标识符**) 的 COM 端口的项值。 端口类安装程序集**PortName**向 COM<em>&lt;n&gt;</em>，其中&lt; *n&gt;* 为 COM 端口号安装程序包含来自[COM 端口数据库](com-port-database.md)。 序列使用此名称来创建到该端口的符号链接。 Windows 支持的 COM 端口数没有限制。 用户模式下客户端使用的符号链接名称以打开 COM 端口。

- 写入下一个条目的值**\\注册表\\机\\硬件\\DeviceMap\\SERIALCOMM**密钥。

  将项值名称是**\\设备\\串行**&lt;*m&gt;，* 其中*&lt;m&gt;* 是分配到设备序列号。 请注意，串行设备数*&lt;m&gt;* 是不相同 COM 端口号 *&lt;n&gt;*。 值**\\设备\\串行**&lt;*m* &gt;设置的值为**PortName**。

- 注册类型的 GUID 的设备接口\_DEVINTERFACE\_COMPORT COM 端口。

  客户端可以注册的 COM 端口接口，抵达的通知，或可以获取所有已注册的 COM 端口接口的符号链接名称。

有关序列如何使用注册表条目值的详细信息，请参阅[序列的注册表设置](registry-settings-for-serial.md)。

 

 




