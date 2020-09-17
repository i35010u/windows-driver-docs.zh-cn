---
title: CD-ROM 实时流式处理
description: 流式传输 (或实时流式处理) 是光盘驱动器提供的一项功能，可实现更快的读取和写入请求。
ms.assetid: A4093485-076A-4414-A3D2-9285B2AC097B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a2d152a7229c98c39e36ca17bb7b5354de5752
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716138"
---
# <a name="span-idstoragecd-rom_real-time_streaming_spancd-rom-real-time-streaming"></a><span id="storage.cd-rom_real-time_streaming_"></span>CD-ROM 实时流式处理


流式传输 (或实时流式处理) 是光盘驱动器提供的一项功能，可实现更快的读取和写入请求。 从 Windows 7 开始，已在存储堆栈的所有层（从 Cdrom.sys 到 Windows Media Player）中实现了对 DVD 视频流的支持，包括 UDF 文件系统驱动程序、Udfs.sys 和视频播放子系统。

## <a name="span-idabout_real-time_streaming_spanspan-idabout_real-time_streaming_spanspan-idabout_real-time_streaming_spanabout-real-time-streaming"></a><span id="About_real-time_streaming_"></span><span id="about_real-time_streaming_"></span><span id="ABOUT_REAL-TIME_STREAMING_"></span>关于实时流式处理


通常，对光学媒体的读写访问权限由两个属性来表征：可靠性和持续性能。 这些属性是相互依赖的，并且不能同时最大化 (更高的可靠性，但会降低性能) 的代价。

适用于光盘媒体的大多数应用程序都专注于可靠性 (也就是说，数据完整性) 。 但是，某些应用程序（如 DVD 刻录机和数字视频摄像机）侧重于持续性能，并需要一定程度的有保证的数据吞吐量才能正确操作。 按照设计，这些应用程序可以灵活应对合理的数据丢失 (例如，视频编解码器假设某些帧可能会丢失) 。 对于这些应用程序，可靠性不是最高优先级。 光驱提供特殊 (所谓的实时流式处理) 操作模式，从而满足此需求。 若要在此模式下提高性能，将忽略读取或写入错误，驱动器不会执行重试或错误纠正或预防。

## <a name="span-iddeveloper_support_for_real-time_streaming_in_windowsspanspan-iddeveloper_support_for_real-time_streaming_in_windowsspanspan-iddeveloper_support_for_real-time_streaming_in_windowsspandeveloper-support-for-real-time-streaming-in-windows"></a><span id="Developer_support_for_real-time_streaming_in_Windows"></span><span id="developer_support_for_real-time_streaming_in_windows"></span><span id="DEVELOPER_SUPPORT_FOR_REAL-TIME_STREAMING_IN_WINDOWS"></span>Windows 中的实时流式处理开发人员支持


从 Windows 7 开始，cd-rom 类驱动程序 Cdrom.sys 支持低级别流式处理读取和写入请求 (MMC 规范) 的 READ12/WRITE12 命令。 用户模式应用程序可使用 [**ioctl \_ CDROM \_ ENABLE \_ 流式处理**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming) i/o 控制代码 (IOCTL) 启用或禁用原始读写请求的流式处理。 这些读写请求是使用为原始 CD/DVD-ROM 设备打开的句柄来执行的。

此外，对于内核模式组件，Cdrom.sys 处理 [**IRP \_ mj \_ READ**](../kernel/irp-mj-read.md) 和 [**IRP \_ mj \_ 写入**](../kernel/irp-mj-write.md) 请求的方式有一些变化。 类驱动程序验证实时流式处理请求是否符合设备的功能。 为了实现此功能，Windows 7 在驱动程序的[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)中引入了一个流式处理标志**SL \_ 实时 \_ 流**。 对于所有流式处理读取或写入请求，将对此标志进行断言，为所有非流式处理请求清除此标志。

存储驱动程序堆栈中的这些更改允许更高的层 (具体而言，文件系统驱动程序和应用程序) 为包含实时数据的文件执行读/写操作。 从 Windows 7 开始，你可以通过使用[**FSCTL \_ 标记 \_ 句柄**](/windows/win32/api/winioctl/ni-winioctl-fsctl_mark_handle)控制代码并通过在[**标记 \_ 句柄 \_ 信息**](/windows/win32/api/winioctl/ns-winioctl-mark_handle_info)结构中设置**标记 \_ 句柄 \_ 实时**标志来指定流模式，从而将文件标记为实时流式处理。

图1说明了常规与流式处理读取和写入请求以及 UDF 文件系统和 CDROM 类驱动程序之间的关系。

![图1： cdrom.sys 和 udfs.sys 中的实时流式处理支持](images/cdromstreaming.png)

DVD 播放应用程序和文件系统驱动程序可以选择使用 IOCTLs 来访问 Cdrom.sys (最低级别) ，或使用 Udfs.sys 中引入的流模式的文件系统支持。 应用程序还可以包含 Windows 视频播放子系统作为整体。 除了播放，Cdrom.sys 和文件系统层还支持流式记录。

## <a name="span-idverifying_device_support_for_real-time_streaming_using_ioctlsspanspan-idverifying_device_support_for_real-time_streaming_using_ioctlsspanspan-idverifying_device_support_for_real-time_streaming_using_ioctlsspanverifying-device-support-for-real-time-streaming-using-ioctls"></a><span id="Verifying_device_support_for_real-time_streaming_using_IOCTLs"></span><span id="verifying_device_support_for_real-time_streaming_using_ioctls"></span><span id="VERIFYING_DEVICE_SUPPORT_FOR_REAL-TIME_STREAMING_USING_IOCTLS"></span>使用 IOCTLs 验证实时流式处理的设备支持


-   使用 [**IOCTL \_ CDROM \_ 获取 \_ 配置**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration) 来确定流功能是否存在以及当前是否存在。

## <a name="span-idenabling_or_disabling_real-time_streaming_using_ioctlsspanspan-idenabling_or_disabling_real-time_streaming_using_ioctlsspanspan-idenabling_or_disabling_real-time_streaming_using_ioctlsspanenabling-or-disabling-real-time-streaming-using-ioctls"></a><span id="Enabling_or_disabling_real-time_streaming_using_IOCTLs"></span><span id="enabling_or_disabling_real-time_streaming_using_ioctls"></span><span id="ENABLING_OR_DISABLING_REAL-TIME_STREAMING_USING_IOCTLS"></span>使用 IOCTLs 启用或禁用实时流式处理


-   使用 [**IOCTL \_ CDROM \_ enable \_ 流式处理**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming) i/o 控制代码启用或禁用原始读写请求的流模式。 此 IOCTL 不具有 output 参数，并且支持将 [**CDROM \_ 流 \_ 控制**](/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_streaming_control) 结构作为输入参数。

    此 IOCTL 基于每个句柄启用或禁用流模式。 默认情况下，对所有新打开的原始 CDROM 句柄禁用流式处理。 不希望使用文件系统并且喜欢使用原始数据的播放应用程序应为同一设备打开两个文件句柄：一个用于文件系统元数据的常规文件句柄和一个用于实时文件的流式处理。

## <a name="span-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspan-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspan-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspecifying-real-time-streaming-for-irp_mj_read-and-irp_mj_write-requests"></a><span id="Specifying_real-time_streaming_for_IRP_MJ_READ_and_IRP_MJ_WRITE_requests"></span><span id="specifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requests"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_IRP_MJ_READ_AND_IRP_MJ_WRITE_REQUESTS"></span>为 IRP \_ mj \_ 读取和 irp \_ mj \_ 写入请求指定实时流式处理


-   \_IoGetCurrentIrpStackLocation 中的 SL 实时 \_ 流标志[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) (irp) &gt; 标志字段控件 ([**Irp \_ mj \_ 读取**](../ifs/irp-mj-read.md)和[**irp \_ mj \_ 写入**](../ifs/irp-mj-write.md)) 读取和写入流式处理请求。 标志设置为所有流式处理读取和写入请求，并清除所有非流式处理请求。 如果设置了 SL \_ 实时 \_ 流标志，Cdrom.sys 将使用 READ12 和 WRITE12 scsi 命令而不是 READ10 或 WRITE10 scsi 命令来执行流式处理请求。 如果 \_ \_ irp 中设置了 SL 实时流标志，但该设备不支持对当前插入的媒体进行流式处理，则将拒绝 irp，状态代码状态 " \_ \_ 设备请求无效" \_ 。

## <a name="span-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspan-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspan-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspecifying-real-time-streaming-for-a-file-using-fsctls"></a><span id="Specifying_real-time_streaming_for_a_file_using_FSCTLs"></span><span id="specifying_real-time_streaming_for_a_file_using_fsctls"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_A_FILE_USING_FSCTLS"></span>使用 FSCTLs 为文件指定实时流式处理


-   可以将任何文件标记为实时读取行为，而不考虑文件类型。 为此，请在[**标记 \_ 控点 \_ 信息**](/windows/win32/api/winioctl/ns-winioctl-mark_handle_info)结构中设置**标记 \_ 句柄 \_ 实时**标志，然后发送[**FSCTL \_ 标记 \_ 句柄**](/windows/win32/api/winioctl/ni-winioctl-fsctl_mark_handle)控制代码。 必须为未缓冲的 i/o 打开用此标志标记的文件。
-   应用程序可以通过在标记句柄信息结构中设置 " **标记 \_ 句柄 \_ 非 \_ 实时** " 标志来取消标记先前标记为实时行为的文件 \_ \_ 。
-   如果 FSCTL \_ 标记 \_ 句柄控制代码通过标记 \_ 句柄 \_ 实时发送，并且 cd-rom/DVD 驱动器或媒体指示不支持实时流式处理功能，则 IOCTL 返回状态 " \_ 无效 \_ 设备 \_ 请求"。 如果在没有缓冲的情况下打开句柄，则 \_ \_ 还会返回状态 "无效的设备 \_ 请求"。

## <a name="span-idperforming_optimum_power_calibration__opc__before_writingspanspan-idperforming_optimum_power_calibration__opc__before_writingspanspan-idperforming_optimum_power_calibration__opc__before_writingspanperforming-optimum-power-calibration-opc-before-writing"></a><span id="Performing_Optimum_Power_Calibration__OPC__before_writing"></span><span id="performing_optimum_power_calibration__opc__before_writing"></span><span id="PERFORMING_OPTIMUM_POWER_CALIBRATION__OPC__BEFORE_WRITING"></span>在写入前 (OPC) 执行最佳电源校准


某些应用程序可能需要预先执行 OPC 过程，以便第一次流式处理写入不必等待 OPC 完成。 为此，Cdrom.sys 提供了一个称为 [**ioctl \_ CDROM \_ SEND \_ OPC \_ 信息**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)的 ioctl。

## <a name="span-iddetermining_the_read_write_speed_for_the_drivespanspan-iddetermining_the_read_write_speed_for_the_drivespanspan-iddetermining_the_read_write_speed_for_the_drivespandetermining-the-readwrite-speed-for-the-drive"></a><span id="Determining_the_read_write_speed_for_the_drive"></span><span id="determining_the_read_write_speed_for_the_drive"></span><span id="DETERMINING_THE_READ_WRITE_SPEED_FOR_THE_DRIVE"></span>确定驱动器的读取/写入速度


MMC 规范建议在使用流式处理 i/o 之前，应用程序指示所需的读取和写入速度，以便驱动器可以在读取和写入质量与吞吐量之间获得更好的平衡。 应用程序可以使用 [**IOCTL \_ CDROM \_ 设置 \_ 速度**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed) 来指示首选速度。 为了确定驱动器支持的功能，Windows 7 引入了 [**IOCTL \_ cdrom \_ 获取 \_ 性能**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance) 控制代码，该代码作为输入 [**CDROM \_ 性能 \_ 请求**](/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_performance_request) 结构。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[**IOCTL \_ CDROM \_ 启用 \_ 流式处理**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)  
[**IOCTL \_ CDROM \_ 获取 \_ 性能**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)  
[**IOCTL \_ CDROM \_ 发送 \_ OPC \_ 信息**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)  
[**IOCTL \_ CDROM \_ 设置 \_ 速度**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)  
[**FSCTL \_ 标记 \_ 句柄**](/windows/win32/api/winioctl/ni-winioctl-fsctl_mark_handle)  
[**标记 \_ 句柄 \_ 信息**](/windows/win32/api/winioctl/ns-winioctl-mark_handle_info)  
[**CDROM \_ 性能 \_ 请求**](/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_performance_request)