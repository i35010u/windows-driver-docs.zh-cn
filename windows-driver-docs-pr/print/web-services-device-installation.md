---
title: 安装打印机支持的设备的 Web 服务
description: 安装打印机支持的设备的 Web 服务
ms.assetid: fb5f043b-bae5-4cb6-95c0-e4e6b9e9d187
keywords:
- Web 服务设备监视器 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bdd818c35832231cead524ead0fb301c2cc22ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381109"
---
# <a name="installing-printers-that-support-web-services-for-devices"></a>安装打印机支持的设备的 Web 服务


网络打印机已启用了 Web Services for Devices (WSD) 可以被发现和通过配对[Windows.Devices.Enumeration](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) API 命名空间。

配对的 WSD 打印机，一旦[WSDMON 端口监视器](wsdmon-port-monitor.md)将自动安装打印机。

有关使用设备枚举和配对的示例**Windows.Devices.Enumeration**，请参阅[设备枚举和配对示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/DeviceEnumerationAndPairing)GitHub 上。

有关详细信息，请参阅[在网络上枚举设备](https://docs.microsoft.com/windows/uwp/devices-sensors/enumerate-devices-over-a-network)Windows SDK 文档中的文章。

 

 




