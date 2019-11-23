---
title: CD-ROM 实时流式处理
description: 流式处理（或实时流式处理）是由光盘驱动器提供的一项功能，可实现更快的读取和写入请求。
ms.assetid: A4093485-076A-4414-A3D2-9285B2AC097B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 585c02a4a388528122707f5650561375c2016324
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841629"
---
# <a name="span-idstoragecd-rom_real-time_streaming_spancd-rom-real-time-streaming"></a><span id="storage.cd-rom_real-time_streaming_"></span>Cd-rom 实时流式处理


流式处理（或实时流式处理）是由光盘驱动器提供的一项功能，可实现更快的读取和写入请求。 从 Windows 7 开始，已在存储堆栈的所有层（从 Cdrom 到 Windows Media Player）中实现了对 DVD 视频流的支持，包括 UDF 文件系统驱动程序、Udf 和视频播放子系统。

## <a name="span-idabout_real-time_streaming_spanspan-idabout_real-time_streaming_spanspan-idabout_real-time_streaming_spanabout-real-time-streaming"></a><span id="About_real-time_streaming_"></span><span id="about_real-time_streaming_"></span><span id="ABOUT_REAL-TIME_STREAMING_"></span>关于实时流式处理


通常，对光学媒体的读写访问权限由两个属性来表征：可靠性和持续性能。 这些属性是相互依赖的，不能同时最大化（更高的可靠性是以较低的性能来实现）。

适用于光盘媒体的大多数应用程序都专注于可靠性（即数据完整性）。 但是，某些应用程序（如 DVD 刻录机和数字视频摄像机）侧重于持续性能，并需要一定程度的有保证的数据吞吐量才能正确操作。 按照设计，这些应用程序可灵活应对合理的数据丢失（例如，视频编解码器假设某些帧可能会丢失）。 对于这些应用程序，可靠性不是最高优先级。 光驱提供操作的特殊（所谓的实时流式处理）模式，从而满足此需求。 若要在此模式下提高性能，将忽略读取或写入错误，驱动器不会执行重试或错误纠正或预防。

## <a name="span-iddeveloper_support_for_real-time_streaming_in_windowsspanspan-iddeveloper_support_for_real-time_streaming_in_windowsspanspan-iddeveloper_support_for_real-time_streaming_in_windowsspandeveloper-support-for-real-time-streaming-in-windows"></a><span id="Developer_support_for_real-time_streaming_in_Windows"></span><span id="developer_support_for_real-time_streaming_in_windows"></span><span id="DEVELOPER_SUPPORT_FOR_REAL-TIME_STREAMING_IN_WINDOWS"></span>Windows 中的实时流式处理开发人员支持


从 Windows 7 开始，cd-rom 类驱动程序（即，MMC 规范的 READ12/WRITE12 命令）支持低级别流式处理读取和写入请求。 用户模式应用程序可以使用[**IOCTL\_CDROM\_启用\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)i/o 控制代码（IOCTL）来启用或禁用原始读写请求的流式处理。 这些读写请求是使用为原始 CD/DVD-ROM 设备打开的句柄来执行的。

此外，对于内核模式组件，Cdrom 处理[**IRP\_mj\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)和[**IRP\_mj\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求。 类驱动程序验证实时流式处理请求是否符合设备的功能。 为实现此功能，Windows 7 在驱动程序的[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)引入了一个流式处理标志， **SL\_实时\_流**。 对于所有流式处理读取或写入请求，将对此标志进行断言，为所有非流式处理请求清除此标志。

存储驱动程序堆栈中的这些更改允许更高的层（特别是文件系统驱动程序和应用程序）以有保证的速度为包含实时数据的文件执行读/写操作。 从 Windows 7 开始，可以通过使用[**FSCTL\_标记\_处理**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_mark_handle)控制代码，并通过在[**标记\_处理\_信息**](https://docs.microsoft.com/windows/desktop/api/winioctl/ns-winioctl-mark_handle_info)结构中设置**mark\_handle\_实时**标志，将文件标记为实时流式处理。

图1说明了常规与流式处理读取和写入请求以及 UDF 文件系统和 CDROM 类驱动程序之间的关系。

![图1： cdrom 和 .sys 中的实时流式处理支持](images/cdromstreaming.png)

DVD 播放应用程序和文件系统驱动程序可以选择使用 IOCTLs 访问 Cdrom 中的原始流式处理支持（最低级别），或使用 Udf 中引入的流模式的文件系统支持。 应用程序还可以包含 Windows 视频播放子系统作为整体。 除了播放，Cdrom .sys 和文件系统层还支持流式记录。

## <a name="span-idverifying_device_support_for_real-time_streaming_using_ioctlsspanspan-idverifying_device_support_for_real-time_streaming_using_ioctlsspanspan-idverifying_device_support_for_real-time_streaming_using_ioctlsspanverifying-device-support-for-real-time-streaming-using-ioctls"></a><span id="Verifying_device_support_for_real-time_streaming_using_IOCTLs"></span><span id="verifying_device_support_for_real-time_streaming_using_ioctls"></span><span id="VERIFYING_DEVICE_SUPPORT_FOR_REAL-TIME_STREAMING_USING_IOCTLS"></span>使用 IOCTLs 验证实时流式处理的设备支持


-   使用[**IOCTL\_CDROM\_获取\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)以确定流功能是否存在以及当前是否存在。

## <a name="span-idenabling_or_disabling_real-time_streaming_using_ioctlsspanspan-idenabling_or_disabling_real-time_streaming_using_ioctlsspanspan-idenabling_or_disabling_real-time_streaming_using_ioctlsspanenabling-or-disabling-real-time-streaming-using-ioctls"></a><span id="Enabling_or_disabling_real-time_streaming_using_IOCTLs"></span><span id="enabling_or_disabling_real-time_streaming_using_ioctls"></span><span id="ENABLING_OR_DISABLING_REAL-TIME_STREAMING_USING_IOCTLS"></span>使用 IOCTLs 启用或禁用实时流式处理


-   使用[**IOCTL\_CDROM\_启用\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)i/o 控制代码，以启用或禁用原始读写请求的流模式。 此 IOCTL 没有 output 参数，并支持[**CDROM\_流式处理\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_streaming_control)结构作为输入参数。

    此 IOCTL 基于每个句柄启用或禁用流模式。 默认情况下，对所有新打开的原始 CDROM 句柄禁用流式处理。 不希望使用文件系统并且喜欢使用原始数据的播放应用程序应为同一设备打开两个文件句柄：一个用于文件系统元数据的常规文件句柄和一个用于实时文件的流式处理。

## <a name="span-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspan-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspan-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspecifying-real-time-streaming-for-irp_mj_read-and-irp_mj_write-requests"></a><span id="Specifying_real-time_streaming_for_IRP_MJ_READ_and_IRP_MJ_WRITE_requests"></span><span id="specifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requests"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_IRP_MJ_READ_AND_IRP_MJ_WRITE_REQUESTS"></span>为 IRP\_MJ 指定实时流式处理\_读取和 IRP\_MJ\_写入请求


-   [**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)（Irp）中的 SL\_实时\_流标志，&gt;的 "标志" 字段控制读写流式处理请求（[**irp\_mj\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)和 irp\_[**写入**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)）。\_ 标志设置为所有流式处理读取和写入请求，并清除所有非流式处理请求。 如果设置了 SL\_实时\_流标志，则 Cdrom .sys 将使用 READ12 和 WRITE12 SCSI 命令而不是 READ10 或 WRITE10 SCSI 命令来执行流式处理请求。 如果在 IRP 中设置了 SL\_实时\_流标志，但该设备不支持对当前插入的媒体进行流式处理，则将拒绝 IRP，状态代码状态为 "\_无效\_设备\_请求"。

## <a name="span-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspan-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspan-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspecifying-real-time-streaming-for-a-file-using-fsctls"></a><span id="Specifying_real-time_streaming_for_a_file_using_FSCTLs"></span><span id="specifying_real-time_streaming_for_a_file_using_fsctls"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_A_FILE_USING_FSCTLS"></span>使用 FSCTLs 为文件指定实时流式处理


-   可以将任何文件标记为实时读取行为，而不考虑文件类型。 为此，请在[**标记\_处理\_信息**](https://docs.microsoft.com/windows/desktop/api/winioctl/ns-winioctl-mark_handle_info)结构中将 "**标记\_句柄"\_实时**标志，然后将[**FSCTL\_MARK**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_mark_handle)发送\_处理控制代码。 必须为未缓冲的 i/o 打开用此标志标记的文件。
-   应用程序可以取消标记先前标记为实时行为的文件，方法是将**标记\_句柄设置\_不\_实时**\_\_标志。
-   如果 FSCTL\_标记\_句柄控制代码随标记\_句柄一起发送\_实时，而 cd-rom/DVD 驱动器或媒体指示不支持实时流式处理功能，则 IOCTL 返回状态\_\_设备\_请求无效。 如果在没有缓冲的情况下打开句柄，则状态\_无效\_设备\_请求也将返回。

## <a name="span-idperforming_optimum_power_calibration__opc__before_writingspanspan-idperforming_optimum_power_calibration__opc__before_writingspanspan-idperforming_optimum_power_calibration__opc__before_writingspanperforming-optimum-power-calibration-opc-before-writing"></a><span id="Performing_Optimum_Power_Calibration__OPC__before_writing"></span><span id="performing_optimum_power_calibration__opc__before_writing"></span><span id="PERFORMING_OPTIMUM_POWER_CALIBRATION__OPC__BEFORE_WRITING"></span>在写入之前执行最佳电源校准（OPC）


某些应用程序可能需要预先执行 OPC 过程，以便第一次流式处理写入不必等待 OPC 完成。 为此，Cdrom 提供了一个名为[**ioctl\_cdrom 的 ioctl\_发送\_OPC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)。

## <a name="span-iddetermining_the_read_write_speed_for_the_drivespanspan-iddetermining_the_read_write_speed_for_the_drivespanspan-iddetermining_the_read_write_speed_for_the_drivespandetermining-the-readwrite-speed-for-the-drive"></a><span id="Determining_the_read_write_speed_for_the_drive"></span><span id="determining_the_read_write_speed_for_the_drive"></span><span id="DETERMINING_THE_READ_WRITE_SPEED_FOR_THE_DRIVE"></span>确定驱动器的读取/写入速度


MMC 规范建议在使用流式处理 i/o 之前，应用程序指示所需的读取和写入速度，以便驱动器可以在读取和写入质量与吞吐量之间获得更好的平衡。 应用程序可以使用[**IOCTL\_CDROM\_将\_速度设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)为指示首选速度。 为了确定驱动器支持的功能，Windows 7 引入了[**IOCTL\_CDROM\_获取\_性能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)控制代码，该代码会将[ **\_性能\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_performance_request)结构作为输入。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[**IOCTL\_CDROM\_启用\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)  
[**IOCTL\_CDROM\_获取\_性能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)  
[**IOCTL\_CDROM\_发送\_OPC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)  
[**IOCTL\_CDROM\_集\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)  
[**FSCTL\_标记\_句柄**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_mark_handle)  
[**标记\_处理\_信息**](https://docs.microsoft.com/windows/desktop/api/winioctl/ns-winioctl-mark_handle_info)  
[**CDROM\_性能\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_performance_request)  



