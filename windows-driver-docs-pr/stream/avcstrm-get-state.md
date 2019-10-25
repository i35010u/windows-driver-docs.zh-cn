---
title: AVCSTRM\_获取\_状态
description: AVCSTRM\_获取\_状态
ms.assetid: f0e73c5f-f1ba-4eb3-ad73-58516f3d1768
keywords:
- AVCSTRM_GET_STATE 流媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_GET_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a09f4f1edb583d604ce506ad2042194cde2ecba9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845028"
---
# <a name="avcstrm_get_state"></a>AVCSTRM\_获取\_状态


## <span id="ddk_avcstrm_get_state_ks"></span><span id="DDK_AVCSTRM_GET_STATE_KS"></span>


**AVCSTRM\_获取\_状态**函数代码获取指定流的当前流状态。

### <a name="io-status-block"></a>I/O 状态块

如果成功， *avcstrm*会将**Irp&gt;IOSTATUS**设置为 STATUS，状态\_SUCCESS。

如果成功，将返回状态\_"成功"。 **CommandData**联合的**StreamState**成员具有当前流状态。 它可以是 KSSTATE\_STOP、KSTATE\_PAUSE 或 KSSTATE\_运行。

可能的错误返回值包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>错误状态</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_DEVICE_REMOVED</p></td>
<td><p>与<strong>AVCSTRM_READ</strong>操作相对应的设备不再存在。</p></td>
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

 

### <a name="comments"></a>备注

此函数使用 AVC\_流\_请求\_块结构中的**CommandData**联合的**StreamState**成员，如下所示。

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
  union _tagCommandData {
    .
    .
    KSSTATE  StreamState;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要求

**标头：** 在*avcstrm*中声明。 包括*avcstrm*。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_STREAM\_请求\_块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、Version 和 Function**  
使用[**INIT\_AVCSTRM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)宏来初始化这些成员。 Pass **AVCSTRM\_获取**宏的 Request 参数\_状态。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定由较早的**AVCSTRM\_OPEN**调用返回的流上下文（句柄），以从获取流状态。

<span id="StreamState"></span><span id="streamstate"></span><span id="STREAMSTATE"></span>**StreamState**  
如果**AVCSTRM\_获取\_状态**成功返回，则此成员包含当前流状态。

子单位驱动程序必须先分配 IRP，并[ **\_流\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)结构。 接下来，它应使用[**INIT\_AVCSTRM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)宏来初始化 AVC\_流\_请求\_块结构，同时传递**AVCSTRM\_获取\_状态**作为宏的请求参数。 接下来，子源驱动程序将**AVCStreamContext**成员设置为要从其获取流状态的流的流上下文（句柄）。

若要发送此请求，子组会将[**irp\_MJ 提交\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)irp，并将 irp 集的**IoControlCode**成员设置为[**IOCTL\_AVCSTRM\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)和**Argument1**IRP 的成员设置为 AVC\_STREAM\_请求\_块结构，该结构描述要从中获取流状态的流。

子单位驱动程序可能希望此命令同步完成。 结果会立即返回，而不会在*avcstrm*中运行挂起的操作。

必须在 IRQL = 被动\_级别调用此函数代码。

### <a name="see-also"></a>另请参阅

[**AVC\_STREAM\_请求\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)， [**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)， [**IRP\_MJ\_内部\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)， [**IOCTL\_AVCSTRM\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [**KSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)、 [**AVCSTRM\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)

 

 





