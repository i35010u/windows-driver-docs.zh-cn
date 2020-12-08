---
title: 初始化包含 WDM 下边缘的微型端口驱动程序
description: 初始化包含 WDM 下边缘的微型端口驱动程序
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，初始化
- NDIS-WDM 微型端口驱动程序 WDK 网络，上边缘
- 微型端口驱动程序 WDK 网络，初始化
- NDIS 微型端口驱动程序 WDK，初始化
- 反序列化 NDIS 微型端口驱动程序 WDK 网络
- NDIS 微型端口驱动程序的下边缘 WDK 网络，驱动程序初始化
- WDM 低边缘 WDK 网络，驱动程序初始化
- 初始化微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df8e9045073f3eaecdfbd01f27f5c6e60fdf52a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803707"
---
# <a name="initializing-a-miniport-driver-with-a-wdm-lower-edge"></a>初始化包含 WDM 下边缘的微型端口驱动程序





操作系统加载了微型端口驱动程序之后，NDIS 将调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数，以初始化微型端口驱动程序管理的微型端口实例。 若要通过具有 WDM 下边缘的微型端口实例进行通信，微型端口驱动程序必须检索特定信息以设置其通信。

在此小型端口实例的初始化过程中，微型端口驱动程序必须调用 [**NdisMGetDeviceProperty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty) 函数来检索通过 WDM 接口设置与微型端口实例的通信所需的设备对象。 在此调用中，微型端口驱动程序将句柄传递到 *MiniportAdapterHandle* 参数中的微型端口实例，并将接收指向 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构的指针的缓冲区传递到该实例。 微型端口驱动程序使用检索到的指向下一设备对象 ( *NextDeviceObject* 参数) 的指针来创建和提交 irp。 有关详细信息，请参阅 [处理 irp](../kernel/handling-irps.md)。

具有 WDM 下边缘的微型端口驱动程序必须是反序列化的微型端口驱动程序。 反序列化的微型端口驱动程序在内部管理其自己的发送和接收请求队列，只要其资源不足，就能立即处理这些请求;如果未反序列化微型端口驱动程序，NDIS 将管理此队列。 必须反序列化 NDIS-WDM 微型端口驱动程序，因为它在 NDIS 调用上下文之外发送和接收数据包。 在小型端口实例的初始化过程中，NDIS-WDM 微型端口驱动程序必须指定反序列化的功能。 反序列化所有 NDIS 6.0 和更高版本的微型端口驱动程序。

请注意，NDIS-WDM 微型端口驱动程序不能是 (驱动程序的中间驱动程序，该驱动程序在顶部公开微型端口驱动程序接口，并在底部) 一个协议驱动程序接口。

 

