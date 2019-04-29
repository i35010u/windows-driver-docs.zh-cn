---
title: AVCSTRM\_CLOSE
description: AVCSTRM\_CLOSE
ms.assetid: 2487ba06-3577-409e-ba82-f9a0d3453c5d
keywords:
- AVCSTRM_CLOSE 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52004cbcd496b68237d120594e7ec038ca6f8004
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371843"
---
# <a name="avcstrmclose"></a>AVCSTRM\_CLOSE


## <span id="ddk_avcstrm_close_ks"></span><span id="DDK_AVCSTRM_CLOSE_KS"></span>


**AVCSTRM\_关闭**函数代码关闭指定的流，并释放 AVCSTRM 中分配的任何资源\_打开。

### <a name="io-status-block"></a>I/O 状态块

如果成功， *avcstrm.sys*设置**Irp-&gt;IoStatus.Status**状态\_成功。

可能的错误返回的值包括：

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
<td><p>设备对应于<strong>AVCSTRM_READ</strong>操作不再存在。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>请求无法完成。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>IRP 中指定的参数不正确，</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>没有足够的系统资源来完成该请求。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>请求已收到但需要进一步处理。 I/O 完成例程将处理最终响应。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用**AVCStreamContext**的成员**CommandData**联合 AVC\_流\_请求\_块结构如下所示。

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

**标头：** 在中声明*avcstrm.h*。 包括*avcstrm.h*。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_流\_请求\_块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、 版本和函数**  
使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化这些成员。 传递**AVCSTRM\_关闭**宏的请求参数中。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定要关闭的流的流上下文 （句柄）。 如果**AVCSTRM\_关闭**成功，返回此值将不再有效。

以下是如何指定要关闭的流的示例：

```cpp
    pAVCStrmReq = &amp;pStrmExt->AVCStrmReq;
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

子单元驱动程序必须首先分配 IRP 和一个[ **AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)结构。 接下来，它应使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化 AVC\_流\_请求\_块结构传递**AVCSTRM\_关闭**为宏的请求参数。 接下来，设置子单元驱动程序**AVCStreamContext**成员添加到要关闭的流。

若要发送此请求，子单元提交[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)与 IRP **IoControlCode** IRP 成员设置为[ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)并**Argument1** IRP 成员设置为AVC\_流\_请求\_描述发生的关闭操作的块结构。

子单元驱动程序可能会以同步方式完成此命令。 挂起的操作中而不立即返回的结果*avcstrm.sys*。

此函数代码必须调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)， [ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)， [ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)， [ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)， [ **AVCSTRM\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 





