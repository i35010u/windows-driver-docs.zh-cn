---
title: 包含设备 Web 服务的 WIA
description: 包含设备 Web 服务的 WIA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3598f28aadcd519e49e1a02ba3960ca200c9c2bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826365"
---
# <a name="wia-with-web-services-for-devices"></a>包含设备 Web 服务的 WIA


在 Windows 中，操作系统支持网络连接的图像扫描程序设备，这些设备实现 (WSD) 的设备的 Web 服务。

WSD 扫描驱动程序是一个收件箱 Microsoft Windows 图像采集 (WIA) 类驱动程序，用于 web 服务扫描程序。 此驱动程序符合用于扫描仪的 Windows 设备协议 (WDP) 。

WSD 扫描驱动程序包包含一种可重复使用的内核驱动程序组件，该组件 *WSDScan.sys* 专门用于安装 web 服务扫描器设备。 

Windows 还包括 *WSD 争取冠军宝座*，它是一种模块，使 web 服务客户端能够质询已断开连接的设备，以便在设备重新联机时重新建立设备通信。

> [!IMPORTANT]  
> 已弃用 WSD 争取冠军宝座功能，并且2018中将删除所有与 WSD 争取冠军宝座相关的文档。

以下各节介绍如何使用 *WSDScan.sys* 为 web 服务扫描程序安装 WIA 驱动程序，如何使用函数发现从 WIA 驱动程序内部使用 scanner 设备初始化 SOAP 通信，以及如何使用 WSD 争取冠军宝座质询已断开连接的设备：

[使用 WSD 安装 WIA 扫描仪驱动程序](installing-a-wia-scanner-driver-with-wsd.md)

[WIA 扫描仪的 SOAP 通信](soap-communications-for-wia-scanners.md)

[使用 WSD 为断开连接的扫描仪提供挑战性](challenging-a-disconnected-scanner-with-the-wsd-challenger.md)

