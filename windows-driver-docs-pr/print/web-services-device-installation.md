---
title: 安装支持设备 Web 服务的打印机
description: 安装支持设备 Web 服务的打印机
keywords:
- Web 服务设备监视器 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43fd6366fb6c105998752bb2028db01e8f5fd631
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785813"
---
# <a name="installing-printers-that-support-web-services-for-devices"></a>安装支持设备 Web 服务的打印机


为 (WSD) 的设备启用了 Web 服务的网络打印机可通过 [Windows.](/uwp/api/Windows.Devices.Enumeration) node.js 命名空间 API 进行查找和配对。

当 WSD 打印机配对后， [WSDMON 端口监视器](wsdmon-port-monitor.md) 会自动安装打印机。

有关使用 **Windows** 的设备枚举和配对的示例，请参阅 GitHub 上的 [设备枚举和配对示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/DeviceEnumerationAndPairing) 。

有关详细信息，请参阅 Windows SDK 文档中的 [通过网络枚举设备一](/windows/uwp/devices-sensors/enumerate-devices-over-a-network) 文。

 

