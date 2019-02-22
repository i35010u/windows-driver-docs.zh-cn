---
title: 设备 MFT 设计指南
description: 本主题概述了可用于执行所有流的后续处理共同点的用户模式下运行的设备级扩展的设计。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: c9af7c1432569a1cfd9c236741410df088294dc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520353"
---
# <a name="device-mft-design-guide"></a>设备 MFT 设计指南

在 Windows 中的视频捕获堆栈 MFT0 形式支持用户模式下扩展。 这是 Ihv 提供，并捕获管道将作为第一个转换后捕获插入的每个流扩展组件。 MFT0 来源设备处理后的帧。 可以在 MFT0 内部完成进一步处理操作，在帧上的文章。 

本主题概述了可用于执行所有流的后续处理共同点的用户模式下运行的设备级扩展的设计。

## <a name="terminology"></a>术语

| 术语       | 描述                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------|
| KS         | 内核流式处理驱动程序                                                                             |
| AvStream   | 音频视频流式处理驱动程序模型                                                                  |
| Filter     | 对象，表示设备实例                                                            |
| 设备 MFT | Ihv 提供的用户模式下捕获驱动程序扩展                                                 |
| Devproxy   | MF <>-AvStream 封送处理程序                                                                           |
| DTM        | 设备转换管理器，用于管理 devproxy 和设备 MFT。 表示 MF 管道中的设备。|

## <a name="design-goals"></a>设计目标

- 具有相同的生存期设备筛选器的设备筛选器范围的用户模式下扩展
- 支持任意数量的输入来自设备
- 支持任意数量的输出 (当前要求是三个流： 预览、 记录和照片)
- 将设备的所有控件都路由到设备 MFT （其中可以选择处理或将其传递到设备）
- 并行后续捕获的流的处理
- 允许在 3A 处理帧速率无关
- 允许从一个流，在其他流之间共享的元数据
- GPU 资源的访问权限
- MF MMCSS 工作队列的访问权限
- MF 分配器的访问
- 简单的界面 （类似于 MFT）
- IHV/OEM 扩展性的灵活的内部体系结构

## <a name="design-constraints"></a>设计的限制

- 捕获 API 图面中的任何更改
- 完成向后兼容性。 例如，无回归时使用的传统应用程序和方案。

## <a name="capture-stack-architecture"></a>捕获堆栈体系结构

本主题介绍对捕获驱动程序的筛选器范围的用户模式下扩展的支持。 此组件有权访问 MF Api，线程池、 GPU 和 ISP 资源。 筛选器宽扩展提供的具有任意数量的流本身和设备 Ks 之间灵活筛选器。 这种灵活性允许带外通信的用户模式下扩展插件和驱动程序可以用于专用元数据和 3A 处理流之间进行无缝。

![捕获堆栈体系结构](images/capture-stack-architecture.png)

<br>
<br>

![设备 mft 体系结构](images/device-mft-architecture.png)

### <a name="device-transform-manager-dtm"></a>设备转换管理器 (DTM)

捕获堆栈引入了新系统提供的组件，设备转换管理器 (DTM)。 这位于 DeviceSource、 管理 Devproxy MFT 和设备 MFT。 DTM 执行 MediaType 协商、 示例传播和所有 MFT 事件处理。 它还公开到 DeviceSource IMFTransform 接口和其他必要的专用接口 DeviceSource 需要管理设备流。 此组件将 Devproxy 和设备 MFT 从管道抽离。 管道只需将 DTM 视为设备和 DTM 超出流作为设备的数据流。

### <a name="devproxy"></a>Devproxy

Devproxy 是异步 MFT 封送的命令和 AvStream 照相机驱动程序和媒体基础的视频帧。 这由 Windows 和支持提供*n*数从照相机驱动程序的输出。 此外，此拥有由设备公开的所有球瓶的分配器。

### <a name="device-mft"></a>设备 MFT

设备 MFT 是捕获驱动程序的用户模式下扩展。 它是*m x n*异步 MFT。 它捕获驱动程序在系统上安装并捕获驱动程序供应商提供。

输入流的设备 MFT 数必须为相同的 Ks pin 由设备公开的数量。 支持的设备 MFT 输入流 mediatypes 必须与公开的 KS pin mediatypes 相同。

公开设备 MFT 的输出流的数量是看到 DeviceSource 和捕获堆栈的数据流、 捕获 API 和应用程序和可以是一个、 两个或三个流。 不需要设备 MFT 的输入和输出流计数相同。 此外，输入和输出流无需具有相同 mediatypes，并且通常将具有不同 mediatypes。 Mediatypes 数不需要与匹配任何一个。

第一个 Ks Pin 由 Devproxy 表示在用户模式下的输出流获取的第一个输入流的设备 MFT，表示用户模式下使用的第二个输入流的设备 MFT，Devproxy 的输出流和等的第二个 Ks Pin 与相关联。

设备 MFT 提供一个指向 Devproxy，DX 设备和 MF 工作队列 id。 来自设备的帧 MF 示例作为反馈直接插入相应设备 MFT 的输入。 与所有这些设备 MFT post 处理捕获的示例以及提供示例预览、 记录和照片的 pin。

所有命令和控件转到设备会重新都路由到设备 MFT。 设备 MFT 处理控件，或将它们传递到通过 Devproxy 驱动程序。 这会简化命令处理了由捕获驱动程序堆栈。

## <a name="functional-overview"></a>功能概述

在捕获管道的初始化，如果该设备，设备 MFT DeviceSource 实例化 DTM。 它将传递到 DTM 的初始化例程表示设备的 Devproxy 的实例。 DTM 共同创建设备 MFT 并执行基本验证，例如，可输出插针的 Devproxy 数相同数量的设备 MFT 输入插针必需接口的支持等。

DeviceSource querys DTM 以获取支持的输出 mediatypes。 DTM 获取这些设备 MFT 输出插针。 Stream 描述符根据此信息来捕获管道和 DeviceSource 公开演示文稿描述符。

SourceReader 使用 DeviceSource 公开的 mediatypes，并在每个流上设置默认 mediatypes。 反过来，DeviceSource DTM 的输出流上设置默认 mediatypes。 DTM 设置上的输出流的设备 MFT 使用 mediatype [SetOutputStreamState](https://msdn.microsoft.com/library/windows/hardware/mt797684)方法。

当**SetOutputStreamState**调用时，若要更改其输入的流的媒体类型到 DTM 消息基于所选的输出媒体类型的设备 MFT 帖子并等待。 响应此消息，DTM querys 的输入流的设备 MFT 使用首选输入 mediatype [GetPreferredInputStreamState](https://msdn.microsoft.com/library/mt797670)。 这对相应的输出流的 Devproxy 设置媒体类型。 如果成功，DTM 对到使用 SetInputStreamState 设备 MFT 输入流设置该相同的媒体类型。 收到此调用后, 完成设备 MFT **SetOutputStreamState**。

CaptureEngine DeviceSource 上的特定流，从而选择各个流。 这将传播到设备 MFT 由通过 DTM **SetOutputStreamState**调用。 设备 MFT 置于请求的状态中特定的输出流。 如上所述，设备 MFT 也会 DTM 通知有关需要启用的必需输入流。 这会导致 DTM 传播 Devproxy 将流选择的内容。 在此过程结束时，所有必要的流，Devproxy 和设备 MFT 中已准备好流式传输。

SourceReader 启动 DeviceSource CaptureEngine 调用 ReadSample 时。 反过来，DeviceSource 将首先发送 MFT_MESSAGE_NOTIFY_BEGIN_STREAMING 和 MFT_MESSAGE_NOTIFY_START_OF_STREAM 消息，指示管道的起始 DTM。 DTM 首先 Devproxy 和设备 MFT 传播 MFT_MESSAGE_NOTIFY_BEGIN_STREAMING 和 MFT_MESSAAGE_NOTIFY_START_OF_STREAM 消息。 

**请注意**分配在启动流式处理而不设备 MFT 初始化所需的资源。

DTM 调用**SetOutputStreamState**上设备 MFT 包含流式处理的状态参数的输出结果。 设备 MFT 开始流式处理在这些输出流中。 DTM 启动流式处理上有有效媒体类型设置 Devproxy 输出流。 Devproxy 分配示例，并从设备提取它们。 这些示例被提供给设备 MFT 中相关的输入插针。 设备 MFT 处理这些示例，并提供 DeviceSource 输出。 从 DeviceSource，这些示例流动到 CaptureEngine SourceReader。

CaptureEngine 停止通过禁用 DeviceSource 上的内部接口通过单个流的各个流。 它将转换为特定的输出流禁用上通过设备 MFT **SetOutputStreamState**。 反过来，设备 MFT 可能会请求禁用特定的输入的流，通过**METransformInputStreamStateChanged**事件。 DTM 将此传播到相应 Devproxy 流。

只要设备 MFT 本身中流式处理状态，则它可以请求的任何输入流转换为任何有效 DeviceStreamState。 例如，它可以将其发送到 DeviceStreamState_Stop 或 DeviceStreamState_Run 或 DeviceStreamState_Pause，以此类推，而不会影响其他流。

但是，由捕获管道控制输出流转换。 例如，预览、 记录和照片流是启用或禁用捕获管道。 输出将被禁用，即使输入的流可能仍流，只要设备 MFT 本身处于流式处理的状态。

![设备 mft 管道预览序列](images/device-mft-pipeline-preview-sequence.png)

<br>
<br>

![设备 mft 采取照片序列](images/device-mft-take-photo-sequence.png)


### <a name="lifetime-of-device-mft"></a>设备 MFT 的生存期

获取创建 KS 筛选器后加载设备 MFT。 获取关闭 KS 筛选器之前，它将被卸载。

从管道的角度，创建 DeviceSource 后，设备 MFT 创建，并且关闭 DeviceSource 时，设备 MFT 关闭同步。

若要支持关机，设备 MFT 必须支持**IMFShutdown**接口。 之后**设备 MFT-> 关闭**调用时，任何其他接口调入设备 MFT 必须返回 MF_E_SHUTDOWN 错误。

### <a name="memory-type"></a>内存类型

可以将帧捕获到系统内存缓冲区或 DX 内存缓冲区，每个照相机的驱动程序的首选项。 任何缓冲区不再是相机驱动程序会直接提供给设备 MFT 进行进一步处理。

Devproxy 将分配基于驱动程序的首选项的缓冲区。 我们需要设备 MFT MF 使用分配器 Api 来分配非就地转换为其输出插针所需的示例。

### <a name="mediatype-change-while-streaming"></a>流式处理时的媒体类型更改

可以看到为本机公开设备 MFT 输出流的 mediatypes 支持 mediatypes SourceReader 的客户端。 本机 mediatype 更改时，SourceReader 将发送到通过 DeviceSource 设备 MFT mediatype 通知调用。 它负责的设备 MFT 以刷新所有挂起的示例从该流的队列并及时地切换到该流上新的媒体类型。 如果必须要更改输入媒体类型，然后它应更改当前的输入媒体类型为一个。 DTM 从设备 MFT 的输入流中获取当前的媒体类型，并将其上 Devproxy 的输出流和设备 MFT 输入设置每个本机媒体类型更改后。

### <a name="input-mediatype-change-in-device-mft"></a>输入设备 MFT 中的媒体类型更改

由于这是*m x n* MFT，可能有负面影响在流式处理的 pin 的 mediatypes 的输入和输出插针的流式处理 mediatypes 时的状态更改或状态更改。 特别是当发生下列变化：

- 输出媒体类型更改

    - 应用程序更改本机媒体类型，它通过级联捕获堆栈到设备 MFT 作为输出媒体类型更改的 pin。

    - 当输出媒体类型的更改，则可能会触发一个输入媒体类型的更改。 例如，假定所有输出插针流式都处理 720p。 这会导致流式处理 720p 照相机中。 接下来，假定记录流更改到 1080p 其本机媒体类型。 在这种情况下，一个到记录流提取数据的设备 MFT 输入流将必须更改其媒体类型。

- 禁用输出插针

    - 当应用程序禁用设备 MFT 输出之一时由多个输出，为了进行优化，共享相同的输入时可能必须输入更改媒体类型。 例如，如果 1080p 输出流停止，并且所有其他流，共享一个输入进行流式处理 720p，则输入的流应将其媒体类型更改为 720p 来节约能源并提高性能。

DTM 句柄[METransformInputStreamStateChanged](https://msdn.microsoft.com/Library/Windows/Hardware/mt797687)通知从设备 MFT，若要更改的媒体类型和设备 MFT 输入以及在这些情况下的 Devproxy 输出的状态。

### <a name="flush-device-mft"></a>刷新设备 MFT

两种类型的刷新需要同时管理设备 MFT:

- 全局刷新

    - 设备 MFT 范围内刷新。 这通常发生在 DTM 将要发送停止流式传输到设备 MFT 的消息。

    - 设备 MFT 应从其输入和输出队列中删除所有示例，并以同步方式返回。

    - 设备 MFT 不应寻求新的输入，或在新的可用输出时发送通知。

- 本地刷新

    - 输出特定于 pin 的刷新。 这通常发生时停止流。

通过设备 MFT 管理器将删除发布之前将刷新的所有事件。 后刷新，设备 MFT 重置其内部[METransformHaveOutput](https://msdn.microsoft.com/library/windows/hardware/mt797686)跟踪计数。

### <a name="drain-of-device-mft"></a>设备 MFT 会被清空

设备 MFT 不会收到 s 单独漏消息由于没有漏实时捕获源中不需要。

### <a name="photo-trigger"></a>照片触发器

在此模型中，而不是发送的照片触发器和照片顺序启动和停止触发器直接向该驱动程序，它们将重新路由到设备 MFT。 设备 MFT 将处理该触发器，或将其转发到根据需要照相机驱动程序。

### <a name="warm-start"></a>热启动

DeviceSource 尝试热启动特定的输出流，通过转换要暂停状态的流。 反过来，调用 DTM [IMFDeviceTransform::SetOutputStreamState](https://msdn.microsoft.com/library/windows/hardware/mt797684)上设备 MFT 转换一个特定的输出流以暂停状态的方法。 这将导致相应的输入流将置于暂停。 这通过设备 MFT 实现通过请求**METransformInputStreamStateChanged** DTM 和处理[IMFDeviceTransform::SetInputStreamState](https://msdn.microsoft.com/library/windows/hardware/mt797683)方法。

### <a name="variable-photo-sequence"></a>可变照片序列

这种体系结构，照片序列是使用摄像机设备驱动程序和设备 MFT，极大地降低了复杂性照相机设备驱动程序实现的。 启动和停止照片序列触发器发送到设备 MFT 并更轻松地处理照片序列。

### <a name="photo-confirmation"></a>照片确认

设备 MFT 支持通过照片确认**IMFCapturePhotoConfirmation**接口。 管道检索通过此接口[IMFGetService::GetService](https://msdn.microsoft.com/library/windows/desktop/ms696978)方法。

### <a name="metadata"></a>元数据

Devproxy 查询元数据的缓冲区大小的驱动程序，并为元数据分配内存。 来自驱动程序的元数据仍由 Devproxy 设置示例。 MFT 设备使用的示例的元数据。 元数据可以通过其输出流示例一起传递或仅用于其后续处理。

支持任意数量的输入设备 MFT，与专用输入插针可以用于只是元数据或带的元数据。 此 pin 的媒体类型是自定义和驱动程序决定的大小和缓冲区的数目。

超出 DTM 公开此元数据的流。 流可以放入设备 MFT 启动流式处理时，流式处理状态。 例如，在流式处理选择输出流，设备 MFT 可以请求 DTM 启动一个或多个视频流和元数据流，使用**METransformInputStreamStateChanged**事件。 

注意：没有任何要求输入 pin 的数量，以匹配输出插针，在此模型中的数。 可以有一个单独的 pin 只是专用于元数据或 3A。

## <a name="device-transform-manager-dtm-event-handling"></a>设备转换管理器 (DTM) 事件处理

[设备转换管理器事件](https://msdn.microsoft.com/Library/Windows/Hardware/mt797660)以下参考主题中定义：

- [METransformFlushInputStream](https://msdn.microsoft.com/library/windows/hardware/mt797685)
- [METransformHaveOutput](https://msdn.microsoft.com/library/windows/hardware/mt797686)
- [METransformInputStreamStateChanged](https://msdn.microsoft.com/Library/windows/hardware/mt797687)
- [METransformNeedInput](https://msdn.microsoft.com/library/windows/hardware/mt797688)


## <a name="imfdevicetransform-interface"></a>IMFDeviceTransform 接口

[IMFDeviceTransform](https://msdn.microsoft.com/library/windows/hardware/mt797663)接口定义与设备 MFT 进行交互。 此接口简化的管理*m*输入并*n*输出设备 MFT。 其他接口，以及设备 MFT 必须实现此接口。

### <a name="general-event-propagation"></a>常规事件传播

事件发生在 Devproxy （或在设备内） 时，我们需要向设备 MFT 和 DeviceSource 传播的。

## <a name="device-mft-requirements"></a>设备 MFT 要求

### <a name="interface-requirements"></a>接口要求

设备 Mft 必须支持以下接口：

- [IMFDeviceTransform](https://msdn.microsoft.com/library/windows/hardware/mt797663)

- [IKsControl](https://msdn.microsoft.com/library/windows/hardware/ff559769)

    - 这允许所有 ksproperties、 事件和方法为通过设备 MFT。 这使设备 MFT 能够处理设备 MFT 这些函数调用或只需将其转发到该驱动程序。 情况下，它将处理 KsEvent 方法，然后设备 MFT 必须执行以下操作：

        - 如果设备 MFT 处理任何**KSEVENT_TYPE_ONESHOT**事件，然后它会在接收时复制句柄**KSEVENT_TYPE_ENABLE**。

        - 当它为已完成的设置或引发事件时，它将调用**CloseHandle**重复句柄。

        - 如果设备 MFT 处理非 KSEVENT_TYPE_ONESHOT 事件，则它应复制句柄，当它收到**KSEVENT_TYPE_ENABLE** ，并调用**CloseHandle**上重复处理当 ks 事件时禁用通过调用 KsEvent 函数中的第一个参数 (ks 事件 id) 和第二个参数 （事件长度） 设置为零。 事件数据和长度才有效。 事件数据中唯一标识特定 ks 事件。

        - 如果设备 MFT 处理非 KSEVENT_TYPE_ONESHOT 事件，则它应复制句柄，当它收到**KSEVENT_TYPE_ENABLE** ，然后应调用**CloseHandle**上重复处理时 ks通过使用设置为零的所有参数调用 KsEvent 函数禁用事件。

- [IMFRealtimeClientEx](https://msdn.microsoft.com/library/windows/desktop/hh448047)

- [IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

- [IMFShutdown](https://msdn.microsoft.com/library/windows/desktop/ms703054)

### <a name="notification-requirements"></a>通知要求

设备 Mft 必须使用以下消息来通知 DTM 的可用性的示例中，任何输入的流状态更改一样，依次类推。

- [METransformHaveOutput](https://msdn.microsoft.com/library/windows/hardware/mt797686)

- [METransformInputStreamStateChanged](https://msdn.microsoft.com/Library/windows/hardware/mt797687)

- [METransformFlushInputStream](https://msdn.microsoft.com/library/windows/hardware/mt797685)

### <a name="thread-requirements"></a>线程要求

设备 MFT 必须创建自己的线程。 它必须改用 MF 工作队列，其 ID 传递[IMFRealtimeClientEx](https://msdn.microsoft.com/library/windows/desktop/hh448047)接口。 这是为了确保在设备 MFT 中运行的所有线程都获取正确的捕获管道运行的优先级。 否则它可能会导致线程优先级倒置。

### <a name="inputstream-requirements"></a>InputStream 要求

#### <a name="stream-count"></a>Stream 计数

- 输入流中设备 MFT 数必须为相同的驱动程序支持的流数。

#### <a name="mediatypes"></a>MediaTypes

- Mediatypes 和支持的设备 MFT 输入实际的媒体类型的数量必须匹配的数量和类型的 mediatypes 驱动程序支持。

- 数可能不同，仅当支持的输入设备 MFT mediatypes 是驱动程序支持 mediatypes 的子集。

- 支持的驱动程序和输入设备 MFT mediatypes 可能是标准或自定义 mediatypes。

### <a name="to-register-device-mft"></a>若要注册设备 MFT

照相机设备 INF 必须具有以下指定的设备 MFT 组件类的 CLSID 的设备接口条目。

```INF
[CaptureAvstrm.Device.NTarm.Interfaces]
AddInterface = %KSCATEGORY_VIDEO_CAMERA%, %Capture.FilterDescBack%, Capture.FilterBack

[Capture.FilterBack]
AddReg = Capture.FilterBack.AddReg, PinNames.AddReg

[Capture.FilterBack.AddReg]
HKR,,FriendlyName,,%Capture.FilterDescBack%
HKR,,CameraDeviceMftClsid,,%CameraDeviceMFT.Clsid%
```

上述 INF 条目会导致以下输入的注册表项：
    
**请注意**这只是一个示例 (不实际 regkey)

```console
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"CameraDeviceMftClsid"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"<<< Device MFT CoClass ID >>>
```
