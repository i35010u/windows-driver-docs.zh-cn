---
title: AVCSTRM \_ 中止 \_ 流式处理
description: AVCSTRM \_ 中止 \_ 流式处理
ms.assetid: 9a136511-c838-456f-87c5-a4639be0c299
keywords:
- AVCSTRM_ABORT_STREAMING 流媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_ABORT_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd604ad5b5fd87d917f26ea80366d3cf0cccf24f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187437"
---
# <a name="avcstrm_abort_streaming"></a>AVCSTRM \_ 中止 \_ 流式处理


## <span id="ddk_avcstrm_abort_streaming_ks"></span><span id="DDK_AVCSTRM_ABORT_STREAMING_KS"></span>


**AVCSTRM \_ 中止 \_ 流式处理**函数代码取消*所有*挂起的数据请求，并释放使用的资源。

### <a name="io-status-block"></a>I/o 状态块

如果成功， *avcstrm.sys* 将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

可能的错误返回值包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>错误状态</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_DEVICE_REMOVED</p></td>
<td><p>与 <strong>AVCSTRM_READ</strong> 操作相对应的设备不再存在。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>无法完成请求。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>IRP 中指定的参数不正确，</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>系统资源不足，无法完成请求。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>已收到请求，但需要进一步处理。 I/o 完成例程将处理最后的响应。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>说明

请注意，此功能将取消 *所有* 流式处理 irp。 若要取消单个 IRP，请使用 [**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)。

删除目标设备或取消原始数据 IRP 以停止流操作时，子单位应调用此操作。

此函数不使用 AVC **CommandData** \_ 流 \_ 请求块结构中的 CommandData 联合的任何成员 \_ 。

```cpp
typedef struct _AVC_STREAM_REQUEST_BLOCK {
  ULONG  SizeOfThisBlock;
  ULONG  Version;
  AVCSTRM_FUNCTION  Function;
  .
  .
  PVOID AVCStreamContext;
  .
  .
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要求

**标头：** 在 *avcstrm*中声明。 包括 *avcstrm*。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC \_ 流 \_ 请求 \_ 块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、Version 和 Function**  
使用 [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header) 宏初始化这些成员。 在宏的 Request 参数中传递 **AVCSTRM \_ ABORT \_ 流式处理** 。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定流上下文 (处理由先前 **AVCSTRM \_ 打开** 调用返回的) ，它是数据写入操作的目标。

子单元驱动程序必须首先分配 IRP 和 [**AVC \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block) 结构。 接下来，它应使用 [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header) 宏来初始化 AVC \_ 流 \_ 请求 \_ 块结构，并 **将 \_ AVCSTRM** 作为 REQUEST 参数传递到宏。 接下来，子单位驱动程序将 **AVCStreamContext** 成员设置为流上下文， (处理流的) 以中止流式处理。

若要发送此请求，子组会 [**将 irp \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md) irp，并将 irp 集的 **IoControlCode** 成员提交给 [**IOCTL \_ AVCSTRM \_ 类**](/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class) ，并将 irp 集的 **Argument1** 成员设置为 AVC \_ 流 \_ 请求 \_ 块结构，该结构描述要发生的中止流式处理操作。

必须在被动级别调用此函数代码 \_ 。 当数据 IRP 被取消时，可以在调度级别执行它 \_ 。 在这种情况下，子单位应启动工作项，并在其工作项例程中调用此函数（在被动级别执行） \_ 。

### <a name="see-also"></a>另请参阅

[**INIT \_AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)， [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)， [**IOCTL \_ AVCSTRM \_ 类**](/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)， [**AVCSTRM \_ 函数**](/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)

 

