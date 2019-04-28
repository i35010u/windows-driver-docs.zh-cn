---
title: 配置为 RS-232 端口即插即用串行设备
description: Plug and Play 串行设备连接到 RS-232 端口的配置
ms.assetid: b6a851e2-0fcf-4d64-80ac-51928b823077
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，插
- RS-232 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8572921ee88246fd0d9a050336803b379e41eef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345019"
---
# <a name="configuration-of-plug-and-play-serial-device-connected-to-an-rs-232-port"></a>Plug and Play 串行设备连接到 RS-232 端口的配置





本部分介绍典型的硬件、 驱动程序和设备堆栈的插串行设备和旧指针设备连接到 RS-232 端口的配置。 可以使用此配置为支持串行设备，如鼠标设备、 指点设备、 图形平板电脑、 调制解调器和数字照相机。

下图显示了插 Toaster 设备的典型配置。

![关系图插 toaster 设备的演示硬件和驱动程序和设备堆栈配置](images/ser2.png)

串行和 Serenum 在以前的配置中使用。 序列创建，并将函数设备对象 (FDO) 附加到 RS-232 端口堆栈和 Serenum 创建，并将较高级别筛选器设备对象 （执行） 附加到 RS-232 端口堆栈。 Serenum 枚举后插 manager 发送 IRP 到 RS-232 端口连接的设备\_MN\_查询\_类型的关系请求**BusRelations**到 RS-232 设备堆栈。

Serenum 检测到受支持的设备后，它创建一个物理设备对象 (PDO)，并报告给插管理器的设备。 Configuration manager 使用此 INF 文件，并为 Toaster 设备安装程序以完成 Toaster 设备安装。 Toaster 驱动程序创建 FDO，并将其附加到 Toaster 设备堆栈。 筛选器 DOs 还可以添加到 Toaster 设备堆栈。

 

 




