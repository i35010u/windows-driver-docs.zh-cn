---
title: 蓝牙配置文件驱动程序简介
description: 蓝牙配置文件驱动程序简介
keywords:
- 蓝牙 WDK，关于蓝牙
- 远程连接 WDK 蓝牙
- 连接 WDK 蓝牙
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4c90a6bc13790c37bd3c72baeaf01139282eed9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784225"
---
# <a name="introduction-to-bluetooth-profile-drivers"></a>蓝牙配置文件驱动程序简介


本部分介绍 Microsoft 为无线蓝牙协议提供的支持。 蓝牙是一种行业标准协议，可用于各种设备（包括计算机、移动电话、手持设备、鼠标设备、键盘和打印机）的无线连接。 本部分还提供了有关如何为启用 Bluetooth 的设备开发蓝牙配置文件驱动程序的指南。 [蓝牙网站上](https://go.microsoft.com/fwlink/p/?linkid=26268)提供了蓝牙协议的详细信息。

Microsoft 在 Microsoft Windows XP Service Pack 2 (SP2) 及更高版本中提供对蓝牙协议的支持。 蓝牙驱动程序称为配置文件驱动程序由独立硬件供应商 (Ihv) 编写，以支持在蓝牙规范中定义的各种协议。 配置文件驱动程序应遵循 Windows 驱动模型 (WDM) 体系结构。

为了支持蓝牙协议，Microsoft 提供了若干驱动程序和支持文件，其中包括：

-   *BthPort.sys*

-   *BthEnum.sys*

-   *BthUsb.sys*

-   *BthProps.cpl*

Ihv 必须使用 Windows Vista 或更高版本来开发其配置文件驱动程序，因为 Windows 的早期版本（包括 Windows XP SP2）不支持配置文件驱动程序开发。

蓝牙驱动程序堆栈提供 (DDIs) 的设备驱动程序接口，该接口允许配置文件驱动程序访问同步 Connection-Oriented (SCO) 链接和逻辑链接控制器以及适配协议 (L2CAP) 本地系统和远程蓝牙设备之间的链接。

### <a name="span-idscospanspan-idscospansco"></a><span id="sco"></span><span id="SCO"></span>**SCO**

面向同步连接的 (SCO) 链接是两个 Bluetooth 设备之间的点到点连接。 它们主要用于支持语音等时间限制的信息。

Windows Vista 蓝牙驱动程序堆栈已增强，可提供 SCO 内核模式 DDIs。 通过使用这些接口，配置文件驱动程序可以使用 SCO DDIs 来打开、更新和关闭 SCO 连接，并通过开放的 SCO 连接执行读取和写入操作。

有关 SCO 的详细信息，请参阅 [创建与远程设备的 Sco 客户端连接](creating-a-sco-client-connection-to-a-remote-device.md) 和 [在蓝牙配置文件驱动程序中接受 sco 连接](accepting-sco-connections-in-a-bluetooth-profile-driver.md)。

### <a name="span-idl2cap_and_sdpspanspan-idl2cap_and_sdpspanl2cap-and-sdp"></a><span id="l2cap_and_sdp"></span><span id="L2CAP_AND_SDP"></span>**L2CAP 和 SDP**

L2CAP 旨在支持 (ACL) 蓝牙链接的异步无连接链接。 蓝牙驱动程序堆栈为面向连接的服务提供支持。 配置文件驱动程序使用 Bluetooth L2CAP DDIs 打开、更新和关闭 L2CAP 连接，并在打开的 L2CAP 连接上执行读取和写入操作。

服务发现协议 (SDP) 为配置文件驱动程序提供了一种方法，用于公布服务或发现它所管理的设备提供的服务。

SDP 记录在复杂字节流中公布。 配置文件驱动程序可以使用 SDP DDIs 来查找 SDP 记录，并将其转换为基于树的表示形式，以便更轻松地进行分析。 配置文件驱动程序还可以使用 SDP DDIs 来构建 SDP 记录的基于树的表示形式，然后将其转换为流以进行播发。

有关 L2CAP 和 SDP 的详细信息，请参阅 [创建与远程设备的 L2CAP 客户端连接](creating-a-l2cap-client-connection-to-a-remote-device.md)、 [在蓝牙配置文件驱动程序中接受 L2CAP 连接](accepting-l2cap-connections-in-a-bluetooth-profile-driver.md) 和 [与 SDP 服务器通信](communicating-with-sdp-servers.md)。

有关蓝牙驱动程序堆栈的详细信息，请参阅 [蓝牙驱动程序堆栈](bluetooth-driver-stack.md)。

 

 





