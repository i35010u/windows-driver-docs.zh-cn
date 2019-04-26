---
title: 初始化包含 WDM 下边缘的微型端口驱动程序
description: 初始化包含 WDM 下边缘的微型端口驱动程序
ms.assetid: 1c5b0ec0-5d63-423d-af21-ffd8990f6160
keywords:
- NDIS WDM 微型端口驱动程序 WDK 连接网络、 初始化
- NDIS WDM 微型端口驱动程序 WDK 网络连接、 上边缘
- 微型端口驱动程序 WDK 连接网络、 初始化
- NDIS 微型端口驱动程序 WDK，初始化
- 反序列化的 NDIS 微型端口驱动程序 WDK 网络
- NDIS 微型端口驱动程序 WDK 网络驱动程序初始化的下边缘
- WDM 低边缘 WDK 网络，驱动程序初始化
- 初始化微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1db5a94c97047f82ac2a1f48b8f64f0b1a6a023
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325010"
---
# <a name="initializing-a-miniport-driver-with-a-wdm-lower-edge"></a>初始化包含 WDM 下边缘的微型端口驱动程序





NDIS 微型端口驱动程序已加载，由操作系统后，调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数以初始化微型端口驱动程序管理的微型端口实例。 若要通过具有 WDM 下边缘的微型端口实例进行通信，微型端口驱动程序必须检索具体的信息来设置其通信。

在初始化期间此微型端口实例，微型端口驱动程序必须调用[ **NdisMGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff563592)函数以检索所需设置与通信的设备对象通过 WDM 界面的微型端口实例。 在此调用中，微型端口驱动程序将句柄传递给微型端口实例*MiniportAdapterHandle*参数和接收指向缓冲区[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构。 微型端口驱动程序将使用下一步设备对象的检索到的指针 ( *NextDeviceObject*参数) 创建和提交 Irp。 有关详细信息，请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)。

使用 WDM 下边缘的微型端口驱动程序必须反序列化的微型端口驱动程序。 反序列化的微型端口驱动程序管理其自身的队列的发送和接收请求在内部，只要有足够的资源来处理这些请求立即;如果微型端口驱动程序不反序列化，NDIS 将管理此队列。 NDIS WDM 微型端口驱动程序必须反序列化，因为它发送和接收数据包的 NDIS 调用上下文之外。 在初始化期间的微型端口实例，NDIS WDM 微型端口驱动程序必须指定反序列化的功能。 所有 NDIS 6.0 和更高版本的微型端口驱动程序被反序列都化。

请注意，NDIS WDM 微型端口驱动程序不能为中间驱动程序 （显示在顶部的微型端口驱动程序接口和协议驱动程序界面底部的驱动程序）。

 

 





