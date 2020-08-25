---
title: 设备 MFT 设计指南
description: 本主题概述了在用户模式下运行的设备范围扩展的设计，该扩展可用于执行所有流通用的后期处理。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: ef0a89ae9c1f974fd7096dd415fdf5c489239b7f
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802749"
---
# <a name="device-mft-design-guide"></a>设备 MFT 设计指南

Windows 中的视频捕获堆栈支持用户模式扩展，格式为 DMFT。 这是 Ihv 提供的每个设备的扩展组件，捕获管道作为首次转换捕获后的内容插入。 DMFT 从设备接收后处理的帧。 可以在 DMFT 中完成对帧的后续处理操作。 DMFT 可以从设备的所有流接收帧，并且可以根据要求公开任意数量的输出流。

本主题概述了在用户模式下运行的设备范围扩展的设计，该扩展可用于执行所有流通用的后期处理。

## <a name="terminology"></a>术语

| 术语       | 说明                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------|
| KS         | 内核流式处理驱动程序                                                                             |
| AvStream   | 音频视频流式处理驱动程序模型                                                                  |
| 筛选器     | 表示设备实例的对象                                                            |
| 设备 MFT | Ihv 提供的用户模式捕获驱动程序扩展                                                 |
| Devproxy   | MF < > AvStream 封送拆收器                                                                           |
| DTM        | 管理 devproxy 和设备 MFT 的设备转换管理器。 表示 MF 管道中的设备。|

## <a name="design-goals"></a>设计目标

- 与设备筛选器生存期相同的设备筛选器范围内用户模式扩展
- 支持来自设备的任意数量的输入
- 支持任意数量的输出 (当前要求为三个流：预览、录制和照片) 
- 将所有设备控件路由到设备 MFT (后者可以选择处理或将其传递到设备) 
- 捕获流的并行后处理
- 允许独立于帧速率的3A 处理
- 允许在其他流之间共享一个流中的元数据
- 访问 GPU 资源
- 对 MF MMCSS 工作队列的访问权限
- 访问 MF 分配器
- 简单界面 (类似于 MFT) 
- 适用于 IHV/OEM 扩展性的灵活内部体系结构

## <a name="design-constraints"></a>设计约束

- 捕获 API 图面上无更改
- 完全向后兼容。 例如，在使用旧的应用和方案时没有回归。

## <a name="capture-stack-architecture"></a>捕获堆栈体系结构

本主题介绍对捕获驱动程序的筛选器范围内用户模式扩展的支持。 此组件可以访问 MF Api、线程池、GPU 和 ISP 资源。 筛选器宽扩展提供了在其自身与 device Ks 筛选器之间具有任意数量的流的灵活性。 这种灵活性允许用户模式扩展与驱动程序之间的无缝带外通信，可用于专用元数据和3A 处理流。

![捕获堆栈体系结构](images/capture-stack-architecture.png)

<br>
<br>

![设备 mft 体系结构](images/device-mft-architecture.png)

### <a name="device-transform-manager-dtm"></a>设备转换管理器 (DTM) 

捕获堆栈引入了一个系统提供的新组件，设备转换管理器 (DTM) 。 它位于 DeviceSource 内，并管理 Devproxy MFT 和设备 MFT。 DTM 执行媒体的协商、示例传播和所有 MFT 事件处理。 它还向 DeviceSource 和 DeviceSource 需要管理设备流的其他必需专用接口公开 IMFTransform 接口。 此组件从管道中提取 Devproxy 和设备 MFT。 管道只是将 DTM 看作设备，并将其作为设备流的流出。

### <a name="devproxy"></a>Devproxy

Devproxy 是一个异步 MFT，用于封送 AvStream 相机驱动程序和媒体基础之间的命令和视频帧。 这是由 Windows 提供的，并支持来自照相机驱动程序的 *n* 个输出。 此外，这还拥有设备公开的所有 pin 的分配器。

### <a name="device-mft"></a>设备 MFT

设备 MFT 是捕获驱动程序的用户模式扩展。 它是一个 *m x n* 异步 MFT。 它使用捕获驱动程序安装在系统上，由捕获驱动程序供应商提供。

设备 MFT 的输入流数量必须与设备公开的 Ks pin 的数目相同。 设备 MFT 的输入流支持的 mediatypes 必须与 KS pin 公开的 mediatypes 相同。

由设备 MFT 公开的输出流的数量是 DeviceSource 和捕获堆栈捕获的流、捕获 API 和应用程序，可以是一个、两个或三个流。 设备 MFT 的输入和输出流计数不必相同。 此外，输入流和输出流不需要具有相同的 mediatypes，并且通常具有不同的 mediatypes。 Mediatypes 数不需要匹配。

Devproxy 的输出流以用户模式表示的第一个 Ks Pin 与设备 MFT 的第一个输入流相关联，第二个 Ks Pin 通过 Devproxy 的输出流以用户模式表示，第二个输入流的设备 MFT 为，依此类推。

为设备 MFT 提供指向 Devproxy、DX 设备和 MF WorkQueue ID 的指针。 设备传出的帧会直接作为 MF 示例送到相应的设备 MFT 输入中。 在所有这些情况下，设备 MFT 都可以对捕获的示例进行 post 处理，并向预览、记录和照片 pin 提供示例。

转到设备的所有命令和控件都将重路由到设备 MFT。 设备 MFT 通过 Devproxy 处理控件或将其传递给驱动程序。 这简化了捕获驱动程序堆栈的命令处理。

## <a name="functional-overview"></a>功能概述

捕获管道初始化时，如果设备有设备 MFT，DeviceSource 会实例化 DTM。 它将表示设备的 Devproxy 的实例传递给 DTM 的初始化例程。 DTM 共同创建设备 MFT 并执行基本验证，例如，verifes Devproxy 的输出插针数量与设备 MFT 的输入插针数量相同，支持强制接口，等等。

DeviceSource querys DTM 以获取支持的输出 mediatypes。 DTM 从设备 MFT 的输出插针获取这些端口。 DeviceSource 根据此信息向捕获管道公开显示描述符和流描述符。

SourceReader 使用 DeviceSource 的公开 mediatypes，并在每个流上设置默认的 mediatypes。 反过来，DeviceSource 将在 DTM 的输出流上设置默认的 mediatypes。 DTM 使用 [SetOutputStreamState](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-setoutputstreamstate) 方法在设备 MFT 的输出流上设置媒体组。

调用 **SetOutputStreamState** 时，设备 MFT 会将消息发布到 DTM，以根据所选的输出媒体媒体和等待更改其输入流的媒体名称。 为响应此消息，DTM 使用 [GetPreferredInputStreamState](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-getinputstreampreferredstate)QUERYS 设备 MFT 输入流的首选输入媒体。 这将在 Devproxy 的相应输出流上设置媒体媒体。 如果成功，则 DTM 使用 SetInputStreamState 将相同的媒体组设置到设备 MFT 的输入流。 收到此调用后，设备 MFT 完成 **SetOutputStreamState**。

CaptureEngine 通过启用 DeviceSource 上的特定流来选择单个流。 这将通过 **SetOutputStreamState** 调用传播到设备 MFT。 设备 MFT 会将特定输出流置于请求状态。 如上所述，设备 MFT 还通知 DTM 有关需要启用的必要输入流。 这会导致 DTM 将选择的流传播到 Devproxy。 在此过程结束时，Devproxy 和设备 MFT 中所有必要的流都已准备好进行流式传输。

SourceReader 在 CaptureEngine 调用 ReadSample 时启动 DeviceSource。 反过来，DeviceSource 通过发送 MFT_MESSAGE_NOTIFY_BEGIN_STREAMING 和 MFT_MESSAGE_NOTIFY_START_OF_STREAM 消息来启动 DTM，该消息指示管道的开头。 DTM 通过传播 MFT_MESSAGE_NOTIFY_BEGIN_STREAMING 和 MFT_MESSAAGE_NOTIFY_START_OF_STREAM 消息来启动 Devproxy 和设备 MFT。 

**注意** 在开始流式处理而不是设备 MFT 初始化时分配所需的资源。

DTM 在带有流式处理状态参数的设备 MFT 输出上调用 **SetOutputStreamState** 。 设备 MFT 开始在这些输出流中进行流式处理。 DTM 在设置了有效媒体类型的 Devproxy 输出流上启动流式处理。 Devproxy 分配示例并从设备获取它们。 这些示例将送进相关输入插针的设备 MFT。 设备 MFT 处理这些示例，并将输出提供给 DeviceSource。 从 DeviceSource 开始，示例通过 SourceReader 流向 CaptureEngine。

CaptureEngine 通过 DeviceSource 上的内部接口禁用各个流来停止单个流。 这将通过 **SetOutputStreamState**转换为设备 MFT 上禁用的特定输出流。 反过来，设备 MFT 可能会通过 **METransformInputStreamStateChanged** 事件请求禁用特定输入流。 DTM 将此传播到相应的 Devproxy 流。

只要设备 MFT 本身处于流式处理状态，它就可以请求将任何输入流转换到任何有效的 DeviceStreamState。 例如，它可以将其发送到 DeviceStreamState_Stop 或 DeviceStreamState_Run 或 DeviceStreamState_Pause 等，而不会影响其他流。

但是，输出流转换由捕获管道控制。 例如，预览版、记录和照片流由捕获管道启用或禁用。 即使输出处于禁用状态，只要设备 MFT 本身处于流式传输状态，输入流仍可进行流式处理。

![设备 mft 管道预览序列](images/device-mft-pipeline-preview-sequence.png)

<br>
<br>

![设备 mft 拍摄照片序列](images/device-mft-take-photo-sequence.png)


### <a name="lifetime-of-device-mft"></a>设备 MFT 的生存期

创建 KS 筛选器后，将加载设备 MFT。 在 KS 筛选器关闭之前，将会将其卸载。

从管道的角度来看，创建 DeviceSource 时，会创建设备 MFT，DeviceSource 关闭后，设备 MFT 会同步关闭。

若要支持关闭，设备 MFT 必须支持 **IMFShutdown** 接口。 在 **设备 mft >关闭** 后，对设备 MFT 的任何其他接口调用都必须返回 MF_E_SHUTDOWN 错误。

### <a name="memory-type"></a>内存类型

根据相机驱动程序的首选项，可以将帧捕获到系统内存缓冲区或 DX 内存缓冲区。 从照相机驱动程序中取出的任何缓冲区会直接送入设备 MFT 进行进一步处理。

Devproxy 将根据驱动程序的首选项分配缓冲区。 需要设备 MFT 才能利用 MF 分配器 Api 为非就地转换分配其输出插针所需的示例。

### <a name="mediatype-change-while-streaming"></a>流式处理时媒体媒体更改

SourceReader 的客户端可以查看由设备 MFT 的输出流公开的 mediatypes 作为本机支持的 mediatypes。 更改本机媒体的媒体时，SourceReader 通过 DeviceSource 将媒体通知调用发送到设备 MFT。 设备 MFT 负责刷新该流的队列中所有挂起的示例并及时切换到该流上的新媒体类型。 如果需要更改输入媒体类型，则应将当前输入类型更改为该输入类型。 DTM 获取设备 MFT 的输入流中的当前媒体数量，并在 Devproxy 的输出流中设置它，并在每个本机媒体的媒体更改后设置设备 MFT 的输入。

### <a name="input-mediatype-change-in-device-mft"></a>设备 MFT 中的输入媒体的更改

由于这是一个 *m x n* MFT，因此在输出流式处理 pin 的 mediatypes 或状态更改时，输入流 pin 的 mediatypes 和状态更改可能会有影响。 具体情况如下：

- 输出媒体的更改

    - 当应用程序更改本机媒体模式时，它会通过捕获堆栈合并到设备 MFT，作为输出插针媒体的媒体更改。

    - 输出媒体的更改时，可能会触发输入媒体的更改。 例如，假定所有输出插针都在720p 流式传输。 这会导致从每个720p 的视频流进行流式处理。 接下来，假定记录流将其本机媒体更改为1080p。 在这种情况下，将数据提取到记录流的设备 MFT 输入流之一必须更改其媒体类型。

- 输出 pin 已禁用

    - 当某个应用程序在多个输出共享同一输入时禁用其中某个设备 MFT 的输出时，为进行优化，输入可能必须更改媒体的媒体。 例如，如果某个1080p 输出流停止，并且所有其他流（共享一个输入）都在720p 进行流式处理，则输入流应将其媒体状态更改为720p，以节省电源和提高性能。

DTM 处理来自设备 MFT 的 [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged) 通知，以便在这些情况下更改设备 mft 输入和 Devproxy 输出上的媒体状态和状态。

### <a name="flush-device-mft"></a>刷新设备 MFT

管理设备 MFT 时需要两种类型的刷新：

- 全局刷新

    - 设备 MFT 范围刷新。 这通常发生在 DTM 即将发送到设备 MFT 的停止流式处理消息时。

    - 设备 MFT 应从其输入和输出队列中删除所有示例，并以同步方式返回。

    - 设备 MFT 不应要求提供新的输入或发送新的可用输出通知。

- 本地刷新

    - 输出插针特定的刷新。 当流停止时，通常会发生这种情况。

在刷新之前发布的所有事件都将被设备 MFT 管理器丢弃。 刷新后，设备 MFT 将重置其内部 [METransformHaveOutput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput) 跟踪计数。

### <a name="drain-of-device-mft"></a>设备 MFT 排出

设备 MFT 不会收到单独的排出消息，因为无需排出实时捕获源。

### <a name="photo-trigger"></a>照片触发器

在此模型中，不会将照片触发器和照片序列直接启动和停止触发器发送到驱动程序，而是将其重新路由到设备 MFT。 设备 MFT 将处理触发器，或根据需要将其转发到相机驱动程序。

### <a name="warm-start"></a>热启动

DeviceSource 尝试通过将流转换为暂停状态来尝试热启动特定的输出流。 接下来，DTM 调用设备 MFT 上的 [IMFDeviceTransform：： SetOutputStreamState](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-setoutputstreamstate) 方法，以将特定的输出流转换为暂停状态。 这会导致将相应的输入流置于暂停。 这是通过将 **METransformInputStreamStateChanged** 请求到 DTM 并处理 [IMFDeviceTransform：： SetInputStreamState](https://docs.microsoft.com/windows/win32/api/mftransform/nf-mftransform-imfdevicetransform-setinputstreamstate) 方法的设备 MFT 实现的。

### <a name="variable-photo-sequence"></a>可变照片序列

利用此体系结构，照片序列是通过相机设备驱动程序和设备 MFT 实现的，这大大降低了照相机设备驱动程序的复杂性。 开始和停止照片序列触发器发送到设备 MFT 并更轻松地处理照片序列。

### <a name="photo-confirmation"></a>照片确认

设备 MFT 通过 **IMFCapturePhotoConfirmation** 接口支持照片确认。 管道通过 [IMFGetService：： GetService](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfgetservice-getservice) 方法检索此接口。

### <a name="metadata"></a>元数据

Devproxy 查询驱动程序的元数据缓冲区大小并为元数据分配内存。 来自驱动程序的元数据仍由示例上的 Devproxy 设置。 设备 MFT 使用示例的元数据。 可以通过示例通过其输出流传递元数据，也可以只将元数据用于其后处理。

使用支持任意数量输入的设备 MFT，专用输入 pin 仅可用于元数据或带外元数据。 此 pin 的媒体大小是自定义的，驱动程序将决定缓冲区的大小和数量。

此元数据流公开了 DTM 以上。 当设备 MFT 开始流式传输时，可以将流置于流式处理状态。 例如，当选择输出流进行流式处理时，设备 MFT 可以通过使用 **METransformInputStreamStateChanged** 事件来请求 DTM 启动一个或多个视频流和元数据流。 

注意：对于此模型中的输出插针数量，不需要输入 pin 的数目。 可以有单独的 pin 专用于元数据或3A。

## <a name="device-transform-manager-dtm-event-handling"></a>设备转换管理器 (DTM) 事件处理

以下参考主题中定义了[设备转换管理器事件](https://docs.microsoft.com/windows-hardware/drivers/stream/device-mft-events)：

- [METransformFlushInputStream](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformflushinputstream)
- [METransformHaveOutput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)
- [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)
- [METransformNeedInput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformneedinput)


## <a name="imfdevicetransform-interface"></a>IMFDeviceTransform 接口

定义 [IMFDeviceTransform](https://docs.microsoft.com/windows/win32/api/mftransform/nn-mftransform-imfdevicetransform) 接口以与设备 MFT 交互。 此接口有助于管理 *m* 输入和 *n* 输出设备 MFT。 除了其他接口，设备 MFT 还必须实现此接口。

### <a name="general-event-propagation"></a>常规事件传播

当 Devproxy (或设备内部发生事件时) 需要将其传播到设备 MFT 和 DeviceSource。

## <a name="device-mft-requirements"></a>设备 MFT 要求

### <a name="interface-requirements"></a>接口要求

设备 MFTs 必须支持以下接口：

- [IMFDeviceTransform](https://docs.microsoft.com/windows/win32/api/mftransform/nn-mftransform-imfdevicetransform)

- [IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-ikscontrol)

    - 这允许所有 ksproperties、事件和方法通过设备 MFT。 这使设备 MFT 能够处理这些函数在设备 MFT 内的调用，或者只是将它们转发给驱动程序。 如果它处理 KsEvent 方法，则设备 MFT 必须执行以下操作：

        - 如果设备 MFT 处理任何 **KSEVENT_TYPE_ONESHOT** 事件，则它会在接收 **KSEVENT_TYPE_ENABLE**时复制句柄。

        - 完成设置或引发事件时，它会对重复的句柄调用 **CloseHandle** 。

        - 如果设备 MFT 处理非 KSEVENT_TYPE_ONESHOT 事件，则它应在接收 **KSEVENT_TYPE_ENABLE** 时复制句柄，并在通过使用第一个参数 (ks 事件 id) 并且第二个参数 (事件长度) 设置为零时调用 KSEVENT 函数来调用 **CloseHandle** 。 事件数据和长度将有效。 事件数据用于唯一标识特定的 ks 事件。

        - 如果设备 MFT 处理非 KSEVENT_TYPE_ONESHOT 事件，则它应在收到 **KSEVENT_TYPE_ENABLE** 时复制句柄，并在通过调用 KSEVENT 函数并将所有参数设置为零来禁用 ks 事件时，应在重复的句柄上调用 **CloseHandle** 。

- [IMFRealtimeClientEx](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfrealtimeclientex)

- [IMFMediaEventGenerator](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

- [IMFShutdown](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfshutdown)

### <a name="notification-requirements"></a>通知要求

设备 MFTs 必须使用以下消息来通知 DTM 有关示例的可用性、任何输入流状态更改等。

- [METransformHaveOutput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)

- [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)

- [METransformFlushInputStream](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformflushinputstream)

### <a name="thread-requirements"></a>线程要求

设备 MFT 不得创建它自己的线程。 相反，它必须使用 MF 工作队列，其 ID 是通过 [IMFRealtimeClientEx](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfrealtimeclientex) 接口传递的。 这是为了确保在设备 MFT 中运行的所有线程获取捕获管道运行时的正确优先级。 否则，可能会导致线程优先级倒置。

### <a name="inputstream-requirements"></a>InputStream 要求

#### <a name="stream-count"></a>流计数

- 设备 MFT 中的输入流数量必须与驱动程序支持的流数量相同。

#### <a name="mediatypes"></a>MediaTypes

- 设备 MFT 输入支持的 mediatypes 数和实际媒体类型必须与该驱动程序支持的 mediatypes 数量和类型匹配。

- 仅当设备 MFT 的输入支持的 mediatypes 是驱动程序支持的 mediatypes 的子集时，此数字才可能不同。

- 驱动程序和设备 MFT 的输入支持的 mediatypes 可以是标准或自定义 mediatypes。

### <a name="to-register-device-mft"></a>注册设备 MFT

照相机设备 INF 必须具有以下设备接口条目，该条目指定设备 MFT 的 CoClass 的 CLSID。

```INF
[CaptureAvstrm.Device.NTarm.Interfaces]
AddInterface = %KSCATEGORY_VIDEO_CAMERA%, %Capture.FilterDescBack%, Capture.FilterBack

[Capture.FilterBack]
AddReg = Capture.FilterBack.AddReg, PinNames.AddReg

[Capture.FilterBack.AddReg]
HKR,,FriendlyName,,%Capture.FilterDescBack%
HKR,,CameraDeviceMftClsid,,%CameraDeviceMFT.Clsid%
```

上述 INF 条目将导致输入以下注册表项：
    
**注意** 这只是一个示例， (不是实际的 regkey) 

```console
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"CameraDeviceMftClsid"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"<<< Device MFT CoClass ID >>>
```
