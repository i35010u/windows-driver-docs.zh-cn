---
title: 创建和启动并行端口
description: 创建和启动并行端口
ms.assetid: 75c82353-6490-47e9-9278-ec0981af9ae9
keywords:
- 并行端口 WDK，创建
- 并行端口 WDK，启动
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fe045b0297f967ee4d0bbd42133a770282fc9f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377543"
---
# <a name="creating-and-starting-a-parallel-port"></a>创建和启动并行端口





插管理器使用的并行端口的系统提供的函数驱动程序的插支持创建和启动函数设备对象 (*FDO*)，表示并行端口。

并行端口功能驱动程序将执行以下操作：

-   创建命名的 FDO

    并行端口设备名称的格式是"\\设备\\ParallelPortx"，其中 x 是端口号的整数值。 并行端口功能驱动程序使用的端口名条目值 (REG\_SZ) 要确定端口号的并行端口插注册表项下。 请注意是否 PortName 具有格式"LPTn"，其中 n 为的端口号，在"ParallePortx"x 设置为 (n-1) 的值。 例如，"ParallelPort0"是"LPT1"与相关联。 如果端口名不具有正确的格式，不创建设备对象。

    请注意，"ParallelPortx"设备名称不能保证。 Microsoft 建议使用[ **IoRegisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification) GUID 抵达的通知\_并行\_设备设备接口。

-   注册并启用一个 GUID\_并行\_的并行端口设备接口

-   验证插管理器发送的资源

-   初始化附加到并行端口 1284.3 设备

    并行端口功能驱动程序的菊花链设备计数，并将菊花链 ID 分配给每个设备。 在 Microsoft Windows 2000 中，该驱动程序分配 Id，从 0 到 3。 在 Windows XP 中，该驱动程序分配一个 ID 为 0 或 1。 设备 Id 将分配给设备按升序排列，开头的设备的物理位置最接近的并行端口。

-   FDO 和关联的 WMI 数据块和回调注册 WDM 提供程序

    并行端口功能驱动程序记录时间分配和释放并行端口的号。

-   确定并行端口硬件支持的通信模式

    硬件必须至少为 IEEE 1284 兼容。 并行端口功能驱动程序进行检查以确定是否在硬件支持字节、 EPP 和 ECP 模式。 请注意，EPP 仅支持一小部分的计算机上。

-   创建并行端口的工作队列 (FIFO)

    每个并行端口都具有其自己的工作队列。 并行端口函数驱动程序队列仅分配，并选择设备的请求。 如果并行端口功能驱动程序收到一个新的分配请求或选择申请时，已分配的端口，它对请求进行排队。

 

 




