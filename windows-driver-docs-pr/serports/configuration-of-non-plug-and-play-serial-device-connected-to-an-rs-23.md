---
title: 配置 RS-232 端口到非 PnP 设备
description: 非即插串行设备连接到 RS-232 端口的配置
ms.assetid: 5106e42e-4f87-47c3-a0ec-f70e77daabd3
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，非即插
- 非即插串行设备 WDK
- RS-232 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 149f929b743235455396cb30cde41e11d8eda0a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522203"
---
# <a name="configuration-of-non-plug-and-play-serial-device-connected-to-an-rs-232-port"></a>非即插串行设备连接到 RS-232 端口的配置





本主题介绍典型的硬件、 驱动程序和设备堆栈的旧串行设备连接到 RS-232 端口的配置。

下图显示了非即插 Toaster 设备的典型配置。

![演示如何硬件和驱动程序和设备堆栈配置非即插 toaster 设备的关系图](images/ser1.png)

Serenum 不用于安装非即插即用串行设备。 安装 Toaster 设备堆栈是特定于设备。 若要与 Toaster 设备进行通信，Toaster 驱动程序将打开[COM 端口](configuration-of-com-ports.md)RS-232 端口与该键相关联。

 

 




