---
title: 蓝牙 HFP DDI IOCTL
description: Windows 8 引入了一组 i/o 控制代码（IOCTLs）作为 DDI 的一部分，它允许音频驱动程序与免提配置文件（HFP）类驱动程序一起使用，以操作蓝牙音频旁路连接。
ms.assetid: 94B6F113-5130-4772-B8A0-5C9992501824
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d5657f26160f5ccfa45276c4b59c772f826224a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833634"
---
# <a name="bluetooth-hfp-ddi-ioctls"></a>蓝牙 HFP DDI IOCTL


Windows 8 引入了一组 i/o 控制代码（IOCTLs）作为 DDI 的一部分，它允许音频驱动程序与免提配置文件（HFP）类驱动程序一起使用，以操作蓝牙音频旁路连接。

除非另有说明，否则本部分中的所有 IOCTLs 均为 true：

-   如果请求成功，则状态\_块结构的信息成员将设置为输出缓冲区的大小（以字节为单位）。 否则，信息成员设置为零。 Status 成员设置为 NTSTATUS 值。

-   所有 IOCTLS 都需要 IRQL &lt;= 被动\_级别。

-   音频驱动程序应使用 IOCTLs 和 IRP\_MJ\_设备\_控制请求。

对于大多数 IOCTL 函数代码，音频驱动程序必须在 HFP 驱动程序的 IO\_堆栈\_位置初始化 FileObject 指针，然后才能将设备控件 IRP 初始化为发送到 HFP 驱动程序。 音频驱动程序通常通过调用 Plxntb 来检索文件对象指针。

音频驱动程序很可能会将其中许多请求发送到任意线程（即 "异步" 请求）。 在这些情况下，音频驱动程序需要使用 IoAllocateIrp 方法构建 IRP 本身，并直接在 IRP 中设置字段，而不是调用 IoBuildDeviceIoControlRequest。

以下主题提供了有关这些 Windows 8 IOCTLs 的更多详细信息：

[**IOCTL\_BTHHFP\_设备\_获取\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)

[**IOCTL\_BTHHFP\_设备\_获取\_VOLUMEPROPERTYVALUES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_volumepropertyvalues)

[**IOCTL\_BTHHFP\_设备\_获取\_KSNODETYPES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_ksnodetypes)

[**IOCTL\_BTHHFP\_设备\_获取\_CONTAINERID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

[**IOCTL\_BTHHFP\_设备\_请求\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect)

[**IOCTL\_BTHHFP\_设备\_请求\_断开连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect)

[**IOCTL\_BTHHFP\_设备\_获取\_连接\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)

[**IOCTL\_BTHHFP\_音箱\_设置\_音量**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_set_volume)

[**IOCTL\_BTHHFP\_发言人\_获取\_批量\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_get_volume_status_update)

[**IOCTL\_BTHHFP\_MIC\_设置\_音量**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_set_volume)

[**IOCTL\_BTHHFP\_MIC\_获取\_卷\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_get_volume_status_update)

[**IOCTL\_BTHHFP\_STREAM\_打开**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)

[**IOCTL\_BTHHFP\_流\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)

[**IOCTL\_BTHHFP\_STREAM\_获取\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)

Windows 8.1 通过添加以下新文件来更新 IOCTLs 集：

[**IOCTL\_BTHHFP\_设备\_获取\_DESCRIPTOR2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor2)

[**IOCTL\_BTHHFP\_设备\_获取\_NRECDISABLE\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_nrecdisable_status_update)

Windows 10 通过添加以下新的一组更新了 IOCTLs：

[**IOCTL\_BTHHFP\_设备\_获取\_编解码器\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_codec_id)

有关使用这些 IOCTLs 的结构的详细信息，请参阅[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)

 

 






