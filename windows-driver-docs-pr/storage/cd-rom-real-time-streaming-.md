---
title: CD-ROM 实时流式处理
description: 流式处理 （或实时流式处理） 是光学介质驱动器允许更快地读取和写入请求提供的功能。
ms.assetid: A4093485-076A-4414-A3D2-9285B2AC097B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aef9449c82b5cc3cd18088ab2057539bd57eacd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544775"
---
# <a name="span-idstoragecd-romreal-timestreamingspancd-rom-real-time-streaming"></a><span id="storage.cd-rom_real-time_streaming_"></span>CD-ROM 实时流式处理


流式处理 （或实时流式处理） 是光学介质驱动器允许更快地读取和写入请求提供的功能。 从 Windows 7 开始，已存储堆栈，从 Windows Media player，包括 UDF 文件系统驱动程序、 Udfs.sys 和视频播放子系统 Cdrom.sys 的所有层中实现的 DVD 视频流式传输的支持。

## <a name="span-idaboutreal-timestreamingspanspan-idaboutreal-timestreamingspanspan-idaboutreal-timestreamingspanabout-real-time-streaming"></a><span id="About_real-time_streaming_"></span><span id="about_real-time_streaming_"></span><span id="ABOUT_REAL-TIME_STREAMING_"></span>有关实时传送视频流


一般情况下，读取和写入访问权限光学媒体的特征是两个属性： 可靠性和维持的性能。 这些属性是相互依赖的并且不能在同一时间 （以较低的性能为代价实现更高的可靠性） 最大化。

大多数应用程序的光学媒体侧重于可靠性 （即，数据完整性）。 但是，某些应用程序，如 DVD 刻录机和数字视频摄像机的重点是维持性能，并且正确操作需要一定的有保证的数据吞吐量。 根据设计，这些应用程序时可复原的合理的数据丢失 （例如，视频编解码器假定一些帧可能会丢失）。 对于这些应用程序，可靠性不是最高优先级。 光盘驱动器满足此需求，通过提供操作的特殊 （所谓实时流式处理） 模式。 若要提高在此模式下的性能、 读取或写入错误会被忽略，并且该驱动器不执行重试或错误纠正或预防。

## <a name="span-iddevelopersupportforreal-timestreaminginwindowsspanspan-iddevelopersupportforreal-timestreaminginwindowsspanspan-iddevelopersupportforreal-timestreaminginwindowsspandeveloper-support-for-real-time-streaming-in-windows"></a><span id="Developer_support_for_real-time_streaming_in_Windows"></span><span id="developer_support_for_real-time_streaming_in_windows"></span><span id="DEVELOPER_SUPPORT_FOR_REAL-TIME_STREAMING_IN_WINDOWS"></span>用于在 Windows 中实时流式处理的开发人员支持


在 Windows 7 中，从 CD-ROM 类驱动程序，Cdrom.sys，支持低级别的流式处理读取和写入请求 （READ12/WRITE12 MMC 规范命令）。 用户模式应用程序可以使用[ **IOCTL\_CDROM\_启用\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/gg441241) I/O 控制代码 (IOCTL) 若要启用或禁用流式处理的原始读取和写入请求数。 使用为原始 CD/DVD-ROM 设备打开的句柄执行以下读取和写入请求。

此外，对于内核模式组件有更改方式 Cdrom.sys 句柄[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)并[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求。 在类驱动程序验证实时流式处理请求符合设备的功能。 若要实现此功能，Windows 7，引入了一个流式处理标志**SL\_实时\_流**中的驱动程序[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659). 此标志添加所有流式处理读取或写入请求，并清除所有非流式处理请求。

存储驱动程序堆栈中的这些更改允许更高版本 （在特定、 文件系统驱动程序和应用程序） 层包含实时数据的文件执行读/写操作的有保证的速度。 从 Windows 7 开始，你可以将标记用于通过使用实时流式处理的文件[ **FSCTL\_标记\_处理**](https://msdn.microsoft.com/library/windows/desktop/aa364576)控制代码，并通过设置指定流式处理模式**MARK\_处理\_实时**中的标志[**标记\_处理\_信息**](https://msdn.microsoft.com/library/windows/desktop/aa365229)结构。

图 1 说明了常规和流式处理读取和写入请求和 UDF 文件系统和 CDROM 类驱动程序之间的关系。

![图 1： 实时流式处理 cdrom.sys 和 udfs.sys 中的支持](images/cdromstreaming.png)

DVD 播放应用程序和文件系统驱动程序可以选择使用 Ioctl 访问 Cdrom.sys （最低级别） 中的原始流支持，或针对流式处理模式中 Udfs.sys 引入使用文件系统支持。 应用程序还可以包括 Windows 视频播放子系统作为一个整体。 除了播放，Cdrom.sys 和文件系统层也支持流式处理记录。

## <a name="span-idverifyingdevicesupportforreal-timestreamingusingioctlsspanspan-idverifyingdevicesupportforreal-timestreamingusingioctlsspanspan-idverifyingdevicesupportforreal-timestreamingusingioctlsspanverifying-device-support-for-real-time-streaming-using-ioctls"></a><span id="Verifying_device_support_for_real-time_streaming_using_IOCTLs"></span><span id="verifying_device_support_for_real-time_streaming_using_ioctls"></span><span id="VERIFYING_DEVICE_SUPPORT_FOR_REAL-TIME_STREAMING_USING_IOCTLS"></span>正在验证的设备支持使用 Ioctl 实时流式处理


-   使用[ **IOCTL\_CDROM\_获取\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff559334)以确定是否存在且当前流式处理功能。

## <a name="span-idenablingordisablingreal-timestreamingusingioctlsspanspan-idenablingordisablingreal-timestreamingusingioctlsspanspan-idenablingordisablingreal-timestreamingusingioctlsspanenabling-or-disabling-real-time-streaming-using-ioctls"></a><span id="Enabling_or_disabling_real-time_streaming_using_IOCTLs"></span><span id="enabling_or_disabling_real-time_streaming_using_ioctls"></span><span id="ENABLING_OR_DISABLING_REAL-TIME_STREAMING_USING_IOCTLS"></span>启用或禁用使用 Ioctl 实时流式处理


-   使用[ **IOCTL\_CDROM\_启用\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/gg441241) I/O 控制代码，以启用或禁用流模式的原始读取和写入请求。 此 IOCTL 不具有输出参数，并支持[ **CDROM\_流式处理\_控制**](https://msdn.microsoft.com/library/windows/hardware/gg441238)作为输入参数的结构。

    此 IOCTL 启用或禁用流模式在每个句柄的基础上。 默认情况下，所有新打开原始 CDROM 句柄的禁用流式处理。 不希望使用文件系统，都喜欢使用原始数据的播放应用程序应打开同一设备的两个文件句柄： 正则另一个用于文件系统元数据和使用一个流式处理进行实时的文件。

## <a name="span-idspecifyingreal-timestreamingforirpmjreadandirpmjwriterequestsspanspan-idspecifyingreal-timestreamingforirpmjreadandirpmjwriterequestsspanspan-idspecifyingreal-timestreamingforirpmjreadandirpmjwriterequestsspanspecifying-real-time-streaming-for-irpmjread-and-irpmjwrite-requests"></a><span id="Specifying_real-time_streaming_for_IRP_MJ_READ_and_IRP_MJ_WRITE_requests"></span><span id="specifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requests"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_IRP_MJ_READ_AND_IRP_MJ_WRITE_REQUESTS"></span>指定实时流式处理 IRP\_MJ\_IRP 读\_MJ\_写入请求


-   SL\_实时\_中的流标志[ **IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)(Irp)-&gt;Flags 字段控件读取和写入流式处理请求 ([ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff549327)并[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff549427))。 该标志设置为所有流式处理读取和写入请求，并清除所有非流式处理请求。 如果 SL\_实时\_设置流标志、 Cdrom.sys 执行流式处理请求而不是 READ10 或 WRITE10 SCSI 命令使用 READ12 和 WRITE12 SCSI 命令。 如果 SL\_实时\_IRP，设置了流标志，但设备不支持当前插入媒体流式处理，IRP 将被拒绝，状态代码状态\_无效\_设备\_请求。

## <a name="span-idspecifyingreal-timestreamingforafileusingfsctlsspanspan-idspecifyingreal-timestreamingforafileusingfsctlsspanspan-idspecifyingreal-timestreamingforafileusingfsctlsspanspecifying-real-time-streaming-for-a-file-using-fsctls"></a><span id="Specifying_real-time_streaming_for_a_file_using_FSCTLs"></span><span id="specifying_real-time_streaming_for_a_file_using_fsctls"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_A_FILE_USING_FSCTLS"></span>指定的文件使用 FSCTLs 实时流式处理


-   可以将标记为实时读取行为，而不考虑文件类型的任何文件。 若要执行此操作，设置**标记\_处理\_实时**标记中[**标记\_处理\_信息**](https://msdn.microsoft.com/library/windows/desktop/aa365229)结构，并然后，将发送[ **FSCTL\_标记\_处理**](https://msdn.microsoft.com/library/windows/desktop/aa364576)控制代码。 必须为无缓冲 I/O 打开使用此标志标记的文件。
-   应用程序可以取消以前标记为实时行为的文件标记通过设置**标记\_处理\_不\_实时**标记中的标志\_句柄\_信息结构。
-   如果 FSCTL\_标记\_句柄的控制代码发送与 MARK\_处理\_实时和 ROM CD/DVD 驱动器或媒体指示不支持实时流式处理功能，IOCTL 返回状态\_无效\_设备\_请求。 如果不进行缓冲，状态打开句柄\_无效\_设备\_请求，也会返回。

## <a name="span-idperformingoptimumpowercalibrationopcbeforewritingspanspan-idperformingoptimumpowercalibrationopcbeforewritingspanspan-idperformingoptimumpowercalibrationopcbeforewritingspanperforming-optimum-power-calibration-opc-before-writing"></a><span id="Performing_Optimum_Power_Calibration__OPC__before_writing"></span><span id="performing_optimum_power_calibration__opc__before_writing"></span><span id="PERFORMING_OPTIMUM_POWER_CALIBRATION__OPC__BEFORE_WRITING"></span>写入之前执行最佳 Power 校准 (OPC)


某些应用程序可能想要提前执行 OPC 过程，以便第一个流写入无需等待 OPC 来完成。 若要执行此操作，Cdrom.sys，提供了名为 IOCTL [ **IOCTL\_CDROM\_发送\_OPC\_信息**](https://msdn.microsoft.com/library/windows/hardware/gg441243)。

## <a name="span-iddeterminingthereadwritespeedforthedrivespanspan-iddeterminingthereadwritespeedforthedrivespanspan-iddeterminingthereadwritespeedforthedrivespandetermining-the-readwrite-speed-for-the-drive"></a><span id="Determining_the_read_write_speed_for_the_drive"></span><span id="determining_the_read_write_speed_for_the_drive"></span><span id="DETERMINING_THE_READ_WRITE_SPEED_FOR_THE_DRIVE"></span>确定驱动器的读/写速度


MMC 规范建议应用程序指示需要读取和写入速度使用流式处理 I/O，因此，在驱动器可以找到之间更好地平衡之前读取和写入质量和吞吐量。 应用程序可以使用[ **IOCTL\_CDROM\_设置\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff559381)以指示首选的速度。 若要确定驱动器的支持的功能，Windows 7 引入了[ **IOCTL\_CDROM\_获取\_性能**](https://msdn.microsoft.com/library/windows/hardware/gg441242)控制代码，将作为输入[ **CDROM\_性能\_请求**](https://msdn.microsoft.com/library/windows/hardware/gg441233)结构。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题
[**IOCTL\_CDROM\_ENABLE\_STREAMING**](https://msdn.microsoft.com/library/windows/hardware/gg441241)  
[**IOCTL\_CDROM\_GET\_PERFORMANCE**](https://msdn.microsoft.com/library/windows/hardware/gg441242)  
[**IOCTL\_CDROM\_SEND\_OPC\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/gg441243)  
[**IOCTL\_CDROM\_SET\_SPEED**](https://msdn.microsoft.com/library/windows/hardware/ff559381)  
[**FSCTL\_MARK\_HANDLE**](https://msdn.microsoft.com/library/windows/desktop/aa364576)  
[**MARK\_处理\_信息**](https://msdn.microsoft.com/library/windows/desktop/aa365229)  
[**CDROM\_PERFORMANCE\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/gg441233)  



