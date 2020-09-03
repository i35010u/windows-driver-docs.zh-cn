---
title: 创建和启动并行端口
description: 创建和启动并行端口
ms.assetid: 75c82353-6490-47e9-9278-ec0981af9ae9
keywords:
- 并行端口 WDK，创建
- 并行端口 WDK，开始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2da462f42b2df0d2702b8acb30ca0e70b13e0b18
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385005"
---
# <a name="creating-and-starting-a-parallel-port"></a>创建和启动并行端口





即插即用 manager 使用系统提供的并行端口函数驱动程序的即插即用支持来创建和启动一个函数设备对象 (*FDO*) ，该对象表示一个并行端口。

并行端口函数驱动程序会执行以下操作：

-   创建名为 FDO 的

    并行端口的设备名称格式为 " \\ device \\ ParallelPortx"，其中 x 是端口号的整数值。 并行端口函数驱动程序使用 \_ 并行端口即插即用注册表项下的 portvalue 项值 (REG SZ) 来确定端口号。 请注意，如果 Portvalue 的格式为 "LPTn"，其中 n 是端口号，则 "ParallePortx" 中的 x 设置为 (n-1) 的值。 例如，"ParallelPort0" 与 "LPT1" 关联。 如果 Portvalue 的格式不正确，则不会创建设备对象。

    请注意，不保证 "ParallelPortx" 设备名称。 Microsoft 建议使用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification) 来通知 GUID \_ 并行 \_ 设备设备接口的到达。

-   为并行端口注册并启用 GUID \_ 并行 \_ 设备接口

-   验证即插即用管理器发送的资源

-   初始化附加到并行端口的1284.3 设备

    并行端口函数驱动程序计算菊花链设备的数目，并为每个设备分配一个菊花链 ID。 在 Microsoft Windows 2000 中，驱动程序将 Id 从0分配给3。 在 Windows XP 中，驱动程序将分配一个0或1的 ID。 设备 Id 按升序分配给设备，从物理上离并行端口最近的设备开始。

-   向 WDM 提供程序注册 FDO 和关联的 WMI 数据块和回调

    并行端口函数驱动程序记录分配和释放并行端口的次数。

-   确定并行端口硬件支持的通信模式

    硬件必须至少为 IEEE 1284 兼容。 并行端口函数驱动程序将进行检查以确定硬件是否支持字节、EPP 和 ECP 模式。 请注意，仅在一小部分计算机上支持 EPP。

-   为并行端口 (FIFO) 创建工作队列

    每个并行端口都有其自己的工作队列。 并行端口功能驱动程序队列仅分配并选择设备请求。 如果在并行端口功能驱动程序收到新的分配请求或选择请求时已分配该端口，则会将该请求排队。

 

