---
title: AVCSTRM\_WRITE
description: AVCSTRM\_WRITE
ms.assetid: de11778d-21ab-40ae-8e7f-5229acfeea42
keywords:
- AVCSTRM_WRITE 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6171fcf669ff755677cdfa6f4428f20a1ab8f7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392112"
---
# <a name="avcstrmwrite"></a>AVCSTRM\_WRITE


## <span id="ddk_avcstrm_write_ks"></span><span id="DDK_AVCSTRM_WRITE_KS"></span>


**AVCSTRM\_编写**函数代码用于提交到指定的流传输的数据缓冲区。

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

此函数使用**BufferStruct**的成员**CommandData**联合 AVC\_流\_请求\_块结构如下所示。

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
    AVCSTRM_BUFFER_STRUCT  BufferStruct;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要求

**标头：** 在中声明*avcstrm.h*。 包括*avcstrm.h*。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_流\_请求\_块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、 版本和函数**  
使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化这些成员。 传递**AVCSTRM\_编写**宏的请求参数中。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定流上下文 （句柄） 返回的早期**AVCSTRM\_打开**，它是调用目标的数据写入操作。

<span id="BufferStruct"></span><span id="bufferstruct"></span><span id="BUFFERSTRUCT"></span>**BufferStruct**  
指定写入操作应从其获取数据的缓冲区。

子单元驱动程序必须首先分配 IRP 和一个[ **AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)结构。 接下来，它应使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化 AVC\_流\_请求\_块结构传递**AVCSTRM\_读取**为宏的请求参数。 接下来，设置子单元驱动程序**AVCStreamContext**流写入数据操作的目标的流上下文 （句柄） 的成员。 最后，将子单元驱动程序设置**BufferStruct**的成员**CommandData**描述缓冲区写入操作的并集获取数据。

若要发送此请求，子单元提交[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)与 IRP **IoControlCode** IRP 成员设置为[ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)并**Argument1** IRP 成员设置为AVC\_流\_请求\_描述发生的写操作的块结构。

此命令以异步方式完成。 完成后，I/O 完成例程中 IRP 设置是名为。

此函数代码必须调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)， [ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)， [ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)， [ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)， [ **AVCSTRM\_缓冲区\_结构**](https://msdn.microsoft.com/library/windows/hardware/ff554108)， [ **AVCSTRM\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 





