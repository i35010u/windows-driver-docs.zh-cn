---
title: AVCSTRM \_ 关闭
description: AVCSTRM \_ 关闭
ms.assetid: 2487ba06-3577-409e-ba82-f9a0d3453c5d
keywords:
- AVCSTRM_CLOSE 流媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a5c80094e5c4f320d1c81cee2ea34d22289f4d4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187433"
---
# <a name="avcstrm_close"></a>AVCSTRM \_ 关闭


## <span id="ddk_avcstrm_close_ks"></span><span id="DDK_AVCSTRM_CLOSE_KS"></span>


**AVCSTRM \_ CLOSE**函数代码关闭指定的流，并释放在 AVCSTRM 中分配的所有资源 \_ 。

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
<th>描述</th>
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

 

### <a name="comments"></a>注释

此函数使用 AVC 流请求块结构中的**CommandData**联合的**AVCStreamContext**成员 \_ ，如下 \_ \_ 所示。

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
使用 [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header) 宏初始化这些成员。 在宏的 Request 参数中传递 **AVCSTRM \_ CLOSE** 。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定流上下文 (处理要关闭的流) 。 如果 **AVCSTRM \_ CLOSE** 成功返回，则此值不再有效。

下面是如何指定要关闭的流的示例：

```cpp
    pAVCStrmReq = &pStrmExt->AVCStrmReq;
    RtlZeroMemory(pAVCStrmReq, sizeof(AVC_STREAM_REQUEST_BLOCK));
    INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_CLOSE);

    pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;

    Status = 
        AVCStrmReqSubmitIrpSynch ( 
            pDevExt->pBusDeviceObject,
            pStrmExt->pIrpReq,
            pAVCStrmReq
            );
```

子单元驱动程序必须首先分配 IRP 和 [**AVC \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block) 结构。 接下来，它应使用 [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header) 宏来初始化 AVC \_ 流 \_ 请求 \_ 块结构，并 **将 \_ AVCSTRM** 作为 REQUEST 参数传递到宏。 接下来，子单位驱动程序将 **AVCStreamContext** 成员设置为要关闭的流。

若要发送此请求，子组会 [**将 \_ irp \_ MJ \_ 内部设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md) irp，并将 irp 集的 **IoControlCode** 成员提交给 [**IOCTL \_ AVCSTRM \_ 类**](/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class) ，并将 irp 集的 **Argument1** 成员提交给 \_ \_ \_ 描述要发生的关闭操作的 AVC 流请求块结构。

子单位驱动程序可能希望此命令同步完成。 结果会立即返回，而不会在 *avcstrm.sys*中挂起操作。

必须在 IRQL = 被动级别调用此函数代码 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)， [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)， [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)， [**IOCTL \_ AVCSTRM \_ 类**](/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)， [**AVCSTRM \_ 函数**](/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)

 

