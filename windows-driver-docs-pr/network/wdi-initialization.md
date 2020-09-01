---
title: Wi-fi 设备初始化
description: 本主题介绍开机后的 Wi-fi 设备初始化。
ms.assetid: EDF04E40-C278-42CE-8E17-F5AB0C1651EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227d4b3c8778e9f1e04906b555d2e102aea8c290
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211551"
---
# <a name="wi-fi-device-initialization"></a>Wi-fi 设备初始化


本主题介绍开机后的 Wi-fi 设备初始化。 开机时，大多数 Wi-fi 设备都处于未初始化模式。 Wi-fi 设备没有足够的 ROM 来容纳固件，因此 IHV 组件/驱动程序会在设备启动过程中使用固件来计划设备。 以下关系图以独立于总线/互连的方式显示初始化顺序。

![wdi 初始化序列](images/wdi-initialization-sequence.png)

1.  IHV 组件负责在适配器启动时将固件下载到适配器。 下载固件的确切机制是依赖于总线的。 此操作在 [*MiniportWdiOpenAdapter*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter) 调用的上下文中完成。 这是一个异步操作。 宿主负责确保在向其发送更多命令之前，适配器已完全初始化并准备好处理命令。 确切的机制依赖于互连。
2.  初始化适配器后，该主机将在适配器中查询各种 Wi-fi 属性、设置属性，并 (Mac) 创建端口，作为小型端口初始化的一部分。
3.  创建并初始化端口后，适配器可以接收任务和属性命令。

 

