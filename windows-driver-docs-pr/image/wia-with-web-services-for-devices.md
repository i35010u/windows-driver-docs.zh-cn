---
title: 包含设备 Web 服务的 WIA
description: 包含设备 Web 服务的 WIA
ms.assetid: e1f91963-503b-4766-a6f1-c334465f0e73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94b977faec1cd5aed54f3b966dd05475142dd423
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577324"
---
# <a name="wia-with-web-services-for-devices"></a>包含设备 Web 服务的 WIA


在 Windows 中，操作系统支持实现 Web Services for Devices (WSD) 的网络连接在一起的映像扫描程序设备。

WSD 扫描驱动程序是 web 服务扫描程序的收件箱 Microsoft Windows 图像采集 (WIA) 类驱动程序。 此驱动程序与兼容的扫描程序使用 Windows 设备协议 (WDP)。

WSD 扫描驱动程序包包含一个可重复使用的内核驱动程序组件， *WSDScan.sys*，即专门用于安装 web 服务扫描程序设备。 

Windows 还包括*WSD 占领*，这是使 web 服务客户端能够挑战断开连接的设备才能重新建立设备通信，当设备重新联机时的模块。

> [!IMPORTANT]  
> WSD 占领功能已弃用，将在 2018年中删除所有与 WSD 占领相关文档。

以下部分介绍如何使用*WSDScan.sys*安装 WIA 驱动程序对 web 服务扫描程序，如何使用功能发现使用扫描程序中的设备从 WIA 驱动程序，初始化 SOAP 通信和操作方法通过使用 WSD 占领质询已断开连接的设备：

[使用 WSD 安装 WIA 扫描程序驱动程序](installing-a-wia-scanner-driver-with-wsd.md)

[WIA 扫描仪的 SOAP 通信](soap-communications-for-wia-scanners.md)

[具有挑战性 WSD 的断开连接的的扫描仪](challenging-a-disconnected-scanner-with-the-wsd-challenger.md)

