---
title: 蓝牙配置文件驱动程序概述
description: 蓝牙配置文件驱动程序概述
ms.assetid: 86806113-28b6-470c-883c-506ac1205f85
keywords:
- 蓝牙 WDK，有关蓝牙
- 远程连接 WDK 蓝牙
- WDK 蓝牙连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 811734c706f25cedaddd03e929ad398456a83cc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520542"
---
# <a name="bluetooth-profile-drivers-overview"></a>蓝牙配置文件驱动程序概述


本部分介绍 Microsoft 提供的用于无线蓝牙协议的支持。 蓝牙是可实现各种设备，包括计算机、 手机、 手持设备、 鼠标设备、 键盘和打印机的无线连接的行业标准协议。 本部分还提供有关如何开发蓝牙已启用蓝牙的设备配置文件的驱动程序的指导原则。 蓝牙协议的详细信息位于[蓝牙](https://go.microsoft.com/fwlink/p/?linkid=26268)网站。

Microsoft 为 Microsoft Windows XP Service Pack 2 (SP2) 和更高版本中的蓝牙协议提供支持。 蓝牙驱动程序，称为配置文件驱动程序编写的独立硬件供应商 (Ihv) 以支持蓝牙规范中定义的各种协议。 配置文件驱动程序应遵循 Windows 驱动程序模型 (WDM) 体系结构。

为了支持蓝牙协议，Microsoft 提供了多个驱动程序和支持文件，其中包括：

-   *BthPort.sys*

-   *BthEnum.sys*

-   *BthUsb.sys*

-   *BthProps.cpl*

Ihv 必须使用 Windows Vista 或更高版本开发其配置文件的驱动程序，因为早期版本的 Windows，包括 Windows XP SP2，不支持配置文件驱动程序开发。

蓝牙驱动程序堆栈提供了启用配置文件驱动程序来访问 Synchronous Connection-Oriented (SCO) 和逻辑链接控制器的本地系统和远程之间的适应协议 (L2CAP) 链接的设备驱动程序接口 (DDIs)蓝牙设备。

### <a name="span-idscospanspan-idscospansco"></a><span id="sco"></span><span id="SCO"></span>**SCO**

同步面向连接的 (SCO) 链接是两个蓝牙设备之间的点对点连接。 定义主要用于支持的有时限的信息，如语音。

Windows Vista 蓝牙驱动程序堆栈已得到增强，以提供 SCO 内核模式 DDIs。 通过使用这些接口，配置文件驱动程序可以使用 SCO DDIs 来打开、 更新和关闭 SCO 连接，以及执行读取和写入操作，通过打开 SCO 连接。

SCO 有关详细信息，请参阅[创建 SCO 客户端连接到远程设备](creating-a-sco-client-connection-to-a-remote-device.md)并[蓝牙配置文件驱动程序中接受 SCO 连接](accepting-sco-connections-in-a-bluetooth-profile-driver.md)。

### <a name="span-idl2capandsdpspanspan-idl2capandsdpspanl2cap-and-sdp"></a><span id="l2cap_and_sdp"></span><span id="L2CAP_AND_SDP"></span>**L2CAP 和 SDP**

L2CAP 设计为支持异步无连接链接 (ACL) 蓝牙链接。 蓝牙驱动程序堆栈的面向连接的服务提供支持。 配置文件驱动程序使用蓝牙 L2CAP DDIs 打开、 更新和关闭 L2CAP 连接并执行读取和写入操作，通过打开 L2CAP 连接。

服务发现协议 (SDP) 提供配置文件的驱动程序公布的服务或发现它所管理的设备提供服务的方法。

SDP 记录就会出现在复杂的字节流中。 配置文件驱动程序可以使用 SDP DDIs 来查找 SDP 记录并将其转换为更轻松地解释用于分析的基于树的表示形式。 配置文件驱动程序可以还使用 SDP DDIs 生成 SDP 记录的基于树的表示形式，并再将其转换为流将该程序播发。

有关 L2CAP 和 SDP 的详细信息，请参阅[创建 L2CAP 客户端连接到远程设备](creating-a-l2cap-client-connection-to-a-remote-device.md)，[蓝牙配置文件驱动程序中接受 L2CAP 连接](accepting-l2cap-connections-in-a-bluetooth-profile-driver.md)和[与通信SDP 服务器](communicating-with-sdp-servers.md)。

蓝牙驱动程序堆栈的详细信息，请参阅[蓝牙驱动程序堆栈](bluetooth-driver-stack.md)。

 

 





