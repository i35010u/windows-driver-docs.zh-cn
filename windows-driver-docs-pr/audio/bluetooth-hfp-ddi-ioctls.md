---
title: 蓝牙 HFP DDI IOCTL
description: Windows 8 引入了一组 i/o 控制代码 (IOCTLs) 作为 DDI 的一部分，它允许音频驱动程序与免提配置文件 (HFP) 类驱动程序一起使用，以操作蓝牙音频旁路连接。
ms.assetid: 94B6F113-5130-4772-B8A0-5C9992501824
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e055b9d81870de02f547084e14d296a836c346d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208233"
---
# <a name="bluetooth-hfp-ddi-ioctls"></a>蓝牙 HFP DDI IOCTL


Windows 8 引入了一组 i/o 控制代码 (IOCTLs) 作为 DDI 的一部分，它允许音频驱动程序与免提配置文件 (HFP) 类驱动程序一起使用，以操作蓝牙音频旁路连接。

除非另有说明，否则本部分中的所有 IOCTLs 均为 true：

-   如果请求成功，则状态块结构的信息成员 \_ 将设置为输出缓冲区的大小（以字节为单位）。 否则，信息成员设置为零。 Status 成员设置为 NTSTATUS 值。

-   所有 IOCTLS 都需要 IRQL &lt; = 被动 \_ 级别。

-   音频驱动程序应使用 IOCTLs 和 IRP \_ MJ \_ 设备 \_ 控制请求。

对于大部分 IOCTL 函数代码， \_ \_ 当音频驱动程序初始化设备控制 IRP 以发送到 HFP 驱动程序时，音频驱动程序必须在 HFP 驱动程序的 IO 堆栈位置初始化 FileObject 指针。 音频驱动程序通常通过调用 Plxntb 来检索文件对象指针。

音频驱动程序很可能会在任意线程上发送很多这些请求 (换言之，"异步" 请求) 。 在这些情况下，音频驱动程序需要使用 IoAllocateIrp 方法构建 IRP 本身，并直接在 IRP 中设置字段，而不是调用 IoBuildDeviceIoControlRequest。

以下主题提供了有关这些 Windows 8 IOCTLs 的更多详细信息：

[**IOCTL \_ BTHHFP \_ 设备 \_ 获取 \_ 描述符**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)

[**IOCTL \_ BTHHFP \_ DEVICE \_ GET \_ VOLUMEPROPERTYVALUES**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_volumepropertyvalues)

[**IOCTL \_ BTHHFP \_ DEVICE \_ GET \_ KSNODETYPES**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_ksnodetypes)

[**IOCTL \_ BTHHFP \_ 设备 \_ 获取 \_ CONTAINERID**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

[**IOCTL \_ BTHHFP \_ 设备 \_ 请求 \_ 连接**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect)

[**IOCTL \_ BTHHFP \_ 设备 \_ 请求 \_ 断开连接**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect)

[**IOCTL \_ BTHHFP \_ DEVICE \_ 获取 \_ 连接 \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)

[**IOCTL \_ BTHHFP \_ 扬声器 \_ 集 \_ 音量**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_set_volume)

[**IOCTL \_ BTHHFP \_ 发言人 \_ 获取 \_ 卷 \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_get_volume_status_update)

[**IOCTL \_ BTHHFP \_ MIC \_ SET \_ 卷**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_set_volume)

[**IOCTL \_ BTHHFP \_ MIC \_ 获取 \_ 卷 \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_get_volume_status_update)

[**IOCTL \_ BTHHFP \_ 流 \_ 打开**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)

[**IOCTL \_ BTHHFP \_ 流 \_ 关闭**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)

[**IOCTL \_ BTHHFP \_ 流 \_ 获取 \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)

Windows 8.1 通过添加以下新文件来更新 IOCTLs 集：

[**IOCTL \_ BTHHFP \_ DEVICE \_ GET \_ DESCRIPTOR2**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor2)

[**IOCTL \_ BTHHFP \_ 设备 \_ 获取 \_ NRECDISABLE \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_nrecdisable_status_update)

Windows 10 通过添加以下新的一组更新了 IOCTLs：

[**IOCTL \_ BTHHFP \_ 设备 \_ 获取 \_ 编解码器 \_ ID**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_codec_id)

有关使用这些 IOCTLs 的结构的详细信息，请参阅 [蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)

 

