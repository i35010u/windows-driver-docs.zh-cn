---
title: 蓝牙 HFP DDI IOCTL
description: Windows 8 引入了一组的 I/O 控制代码 (Ioctl)，允许音频驱动程序能够在无需手动配置文件 (HFP) 类驱动程序，运行蓝牙音频绕过连接使用 DDI 的一部分。
ms.assetid: 94B6F113-5130-4772-B8A0-5C9992501824
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fd9c072aa55f89a74baa2f46bcc7d96fc03de9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355611"
---
# <a name="bluetooth-hfp-ddi-ioctls"></a>蓝牙 HFP DDI IOCTL


Windows 8 引入了一组的 I/O 控制代码 (Ioctl)，允许音频驱动程序能够在无需手动配置文件 (HFP) 类驱动程序，运行蓝牙音频绕过连接使用 DDI 的一部分。

除非另行说明，下面是适用于在本部分中的所有 Ioctl:

-   如果请求成功，状态信息成员\_块结构设置为，以字节为单位的输出缓冲区的大小。 否则，将信息成员设置为零。 状态成员设置为 NTSTATUS 值。

-   所有 IOCTL 都需要 IRQL &lt;= 被动\_级别。

-   音频驱动程序应使用 IRP Ioctl\_MJ\_设备\_控制请求。

对于大多数 IOCTL 函数代码，音频驱动程序必须进行初始化的 IO 中的文件对象指针\_堆栈\_HFP 驱动程序音频驱动程序初始化设备控制 IRP 将发送到 HFP 驱动程序时的位置。 音频驱动程序通常通过调用 IoGetDeviceObjectPointer 检索对象的指针。

音频驱动程序可能会发送很多这些请求在任意线程 （即，"异步"请求）。 在这些情况下，音频驱动程序将需要生成 IRP 本身使用 IoAllocateIrp 方法，并在而调用 IoBuildDeviceIoControlRequest IRP 直接设置字段。

以下主题提供有关这些 Windows 8 Ioctl 的更多详细信息：

[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_VOLUMEPROPERTYVALUES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_volumepropertyvalues)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_KSNODETYPES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_ksnodetypes)

[**IOCTL\_BTHHFP\_设备\_获取\_CONTAINERID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

[**IOCTL\_BTHHFP\_设备\_请求\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect)

[**IOCTL\_BTHHFP\_DEVICE\_REQUEST\_DISCONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CONNECTION\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)

[**IOCTL\_BTHHFP\_演讲者\_设置\_卷**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_set_volume)

[**IOCTL\_BTHHFP\_演讲者\_获取\_卷\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_get_volume_status_update)

[**IOCTL\_BTHHFP\_MIC\_SET\_VOLUME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_set_volume)

[**IOCTL\_BTHHFP\_MIC\_GET\_VOLUME\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_get_volume_status_update)

[**IOCTL\_BTHHFP\_STREAM\_OPEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)

[**IOCTL\_BTHHFP\_STREAM\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)

[**IOCTL\_BTHHFP\_STREAM\_GET\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)

Windows 8.1 已通过添加以下新的更新的一套 Ioctl:

[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor2)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_NRECDISABLE\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_nrecdisable_status_update)

Windows 10 已通过添加以下新一个更新的一套 Ioctl:

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CODEC\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_codec_id)

有关使用这些 Ioctl 的结构的信息，请参阅[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)

 

 






