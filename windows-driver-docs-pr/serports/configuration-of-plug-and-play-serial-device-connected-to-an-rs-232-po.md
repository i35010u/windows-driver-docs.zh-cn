---
title: 将 PnP 串行设备配置为 RS-232 端口
description: 即插即用串行设备连接到 RS-232 端口的配置
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
- RS-232 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 397c4a433ec266172266902c7c2292ba006b5940
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812071"
---
# <a name="configuration-of-plug-and-play-serial-device-connected-to-an-rs-232-port"></a>即插即用串行设备连接到 RS-232 端口的配置





本部分介绍即插即用串行设备的硬件、驱动程序和设备堆栈的典型配置，以及连接到 RS-232 端口的旧指针设备。 此配置可用于支持串行设备，例如鼠标设备、指针设备、绘图板、调制解调器和数字照相机。

下图显示了即插即用 Toaster 设备的典型配置。

![说明即插即用 toaster 设备的硬件和驱动程序和设备堆栈配置的示意图](images/ser2.png)

串行和 Serenum 用于前面的配置。 串行创建 (FDO) 的函数设备对象并将其附加到 RS-232 端口堆栈，Serenum 创建并附加上层筛选器设备对象， (将) 到 RS-232 端口堆栈。 Serenum 在即插即用 manager 将 \_ BusRelations 类型的 IRP MN \_ 查询 \_ 关系请求发送到 rs-232 设备堆栈 **BusRelations** 后，枚举附加到 rs-232 端口的设备。

Serenum 检测到受支持的设备后，它将创建 (PDO) 的物理设备对象，并将设备报告给即插即用 manager。 配置管理器使用 INF 文件和 Toaster 设备的安装程序来完成 Toaster 设备安装。 Toaster 驱动程序创建 FDO 并将其附加到 Toaster 设备堆栈。 还可以将筛选器 DOs 添加到 Toaster 设备堆栈中。

 

 




