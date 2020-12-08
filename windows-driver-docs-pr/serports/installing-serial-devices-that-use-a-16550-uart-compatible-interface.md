---
title: 使用 16550 UART-Compatible 接口安装串行设备
description: 安装使用 16550 UART 兼容接口的串行设备
keywords:
- 串行驱动程序 WDK，16550 UART 兼容接口
- 通用异步接收器-发射器 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容的接口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d473598b727e3a2931918954151d949dc112a508
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812007"
---
# <a name="installing-serial-devices-that-use-a-16550-uart-compatible-interface"></a>安装使用 16550 UART 兼容接口的串行设备

若要安装使用串行作为低级设备筛选器驱动程序的即插即用设备，请执行以下操作：

- 将 "串行" 指定为设备的 INF 文件中的较低级别的设备筛选器驱动程序-请参阅 [安装筛选器驱动程序](../install/installing-a-filter-driver.md)。

- 将设备的 **SerialSkipExternalNaming** 输入值设置为非零值--请参阅 [即插即用串行设备的注册表设置](registry-settings-for-a-plug-and-play-serial-device.md)。
