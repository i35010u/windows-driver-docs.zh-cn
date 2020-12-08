---
title: 将非 PnP 设备配置为 RS-232 端口
description: 配置连接到232端口的非即插即用串行设备
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，非即插即用
- 非即插即用串行设备 WDK
- RS-232 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 061e6b7412d6b85a8b647e9c7cc90fc56aa4d4eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812075"
---
# <a name="configuration-of-non-plug-and-play-serial-device-connected-to-an-rs-232-port"></a>配置连接到232端口的非即插即用串行设备





本主题介绍连接到 RS-232 端口的旧版串行设备的硬件、驱动程序和设备堆栈的典型配置。

下图显示了非即插即用 Toaster 设备的典型配置。

![说明非即插即用 toaster 设备的硬件和驱动程序和设备堆栈配置的示意图](images/ser1.png)

Serenum 不用于安装非即插即用串行设备。 Toaster 设备堆栈的安装是特定于设备的。 若要与 Toaster 设备通信，Toaster 驱动程序会打开与 RS-232 端口关联的 [COM 端口](configuration-of-com-ports.md) 。

 

 




