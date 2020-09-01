---
title: 使用 16550 UART 兼容的接口安装串行设备
description: 安装使用 16550 UART 兼容接口的串行设备
ms.assetid: d80db651-b890-44dc-98ad-32e72e244d8c
keywords:
- 串行驱动程序 WDK，16550 UART 兼容接口
- 通用异步接收器-发射器 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容的接口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 290a4765a5d05a0d70cd1831237b41dbbbb5d095
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186971"
---
# <a name="installing-serial-devices-that-use-a-16550-uart-compatible-interface"></a>安装使用 16550 UART 兼容接口的串行设备

若要安装使用串行作为低级设备筛选器驱动程序的即插即用设备，请执行以下操作：

- 将 "串行" 指定为设备的 INF 文件中的较低级别的设备筛选器驱动程序-请参阅 [安装筛选器驱动程序](../install/installing-a-filter-driver.md)。

- 将设备的 **SerialSkipExternalNaming** 输入值设置为非零值--请参阅 [即插即用串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。