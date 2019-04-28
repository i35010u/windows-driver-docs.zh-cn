---
title: 使用 16550 UART 兼容接口安装串行设备
description: 安装使用 16550 UART 兼容接口的串行设备
ms.assetid: d80db651-b890-44dc-98ad-32e72e244d8c
keywords:
- 串行驱动程序 WDK，16550 UART 兼容接口
- 通用的异步接收方发射机 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容接口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa98a5ba8cce978138a7065463ab199e7a46f960
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331148"
---
# <a name="installing-serial-devices-that-use-a-16550-uart-compatible-interface"></a>安装使用 16550 UART 兼容接口的串行设备





若要安装即插即用设备使用序列作为较低级别设备筛选器驱动程序，请执行以下操作：

-   指定序列作为设备的 INF 文件中的较低级别设备筛选器驱动程序--请参阅[安装筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff547595)。

-   设置**SerialSkipExternalNaming**条目值，该设备为非零值-请参阅[即插即用和播放串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。

 

 




