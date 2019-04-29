---
title: AVCSTRM\_ABORT\_STREAMING
description: AVCSTRM\_ABORT\_STREAMING
ms.assetid: 9a136511-c838-456f-87c5-a4639be0c299
keywords:
- AVCSTRM_ABORT_STREAMING 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_ABORT_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d5bd3091accebe678cf577eb54761bdb78790ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390196"
---
# <a name="avcstrmabortstreaming"></a>AVCSTRM\_ABORT\_STREAMING


## <span id="ddk_avcstrm_abort_streaming_ks"></span><span id="DDK_AVCSTRM_ABORT_STREAMING_KS"></span>


**AVCSTRM\_中止\_流式处理**函数代码取消*所有*挂起的数据请求，并释放使用的资源。

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

请注意，此功能取消*所有*流式处理 Irp。 若要取消单个 IRP，请使用[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)。

删除其目标设备或原始数据 IRP 取消停止流操作时，子单元应调用此成员。

此函数不使用的任何成员**CommandData** AVC 联合\_流\_请求\_块结构。

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
使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化这些成员。 传递**AVCSTRM\_中止\_流式处理**宏的请求参数中。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定流上下文 （句柄） 返回的早期**AVCSTRM\_打开**，它是调用目标的数据写入操作。

子单元驱动程序必须首先分配 IRP 和一个[ **AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)结构。 接下来，它应使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化 AVC\_流\_请求\_块结构传递**AVCSTRM\_读取**为宏的请求参数。 接下来，设置子单元驱动程序**AVCStreamContext**成员添加到流的流上下文 （句柄） 中止流式处理。

若要发送此请求，子单元提交[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)与 IRP **IoControlCode** IRP 成员设置为[ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)并**Argument1** IRP 成员设置为AVC\_流\_请求\_描述流式处理操作发生该中止的块结构。

必须在被动调用此函数代码\_级别。 当取消 IRP 数据时，它可以执行在调度\_级别。 在这种情况下，子单元应启动的工作项并调用其工作项例行，这在被动执行此函数\_级别。

### <a name="see-also"></a>请参阅

[**INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)， [ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)， [ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)， [ **AVCSTRM\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 





