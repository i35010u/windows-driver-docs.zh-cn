---
title: AVCSTRM\_OPEN
description: AVCSTRM\_OPEN
ms.assetid: d352615b-8ab8-40ac-b165-479686abd587
keywords:
- AVCSTRM_OPEN 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_OPEN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28a3dd4abe1e4fb2a76fa75366758d386a7810fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374496"
---
# <a name="avcstrmopen"></a>AVCSTRM\_OPEN


## <span id="ddk_avcstrm_open_ks"></span><span id="DDK_AVCSTRM_OPEN_KS"></span>


**AVCSTRM\_打开**函数代码与特定的流格式打开一个流。

### <a name="io-status-block"></a>I/O 状态块

如果成功， *avcstrm.sys*设置**Irp-&gt;IoStatus.Status**状态\_成功。

如果成功，状态\_与流上下文中一起返回成功**AVCStreamContext**的成员[ **AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)结构。 对于其他随后使用此上下文*avcstrm.sys*请求。

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

此函数使用**OpenStruct**的成员**CommandData**联合 AVC\_流\_请求\_块结构如下所示。

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
    AVCSTRM_OPEN_STRUCT  OpenStruct;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要求

**标头：** 在中声明*avcstrm.h*。 包括*avcstrm.h*。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_流\_请求\_块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、 版本和函数**  
使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化这些成员。 传递**AVCSTRM\_打开**宏的请求参数中。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定的流上下文 （句柄）。 这应该是**NULL**在输入时，如果**AVCSTRM\_打开**成功，返回此成员包含有效的流上下文后续*avcstrm.sys*操作。

<span id="OpenStruct"></span><span id="openstruct"></span><span id="OPENSTRUCT"></span>**OpenStruct**  
指定要创建的 AV/C 流的说明。

[ **AVCSTRM\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff554114)枚举提供支持的 AV/C 流式处理格式 （从 IEC 61883 规范中） 的列表*avcstrm.sys*支持，如 SDDV (61883-2) 和 MPEG2TS (61883-4)。

若要使同步连接、 CIP 标头和次级单位依赖参数所需和中定义[ **AVCSTRM\_格式\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554117)结构。

下面是用于接收数据的 MPEG2TS 格式信息的示例：

```cpp
//
// MPEG2TS
//
    { 
        sizeof(AVCSTRM_FORMAT_INFO),
        AVCSTRM_FORMAT_MPEG2TS,
        {
            0,0,
            CIP_SPH_MPEG, 
            CIP_QPC_MPEG,
            CIP_FN_MPEG,
            IP_DBS_MPEG,
            0,0
        }, // CIP header[0]
        {
            0,0,0,
            CIP_TSF_OFF,
            CIP_FMT_MPEG,
            2,
        },  // CIP header[1]
        SRC_PACKETS_PER_MPEG2TS_FRAME,   // varies depending on number of source packets
        BUFFER_SIZE_MPEG2TS_NO_SPH,   // Remove source packet header
        NUM_OF_XMT_BUFFERS_MPEG2TS,   // Subunit defined
        0,
        FALSE, // not striping SPH is the default
        0,  
        BLOCK_PERIOD_MPEG2TS, // 192, / number of 1394 cycle offset to send one block
        0,0,0,0,
    },
```

子单元驱动程序必须首先分配 IRP 和一个[ **AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)结构。 接下来，它应使用[ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)宏来初始化 AVC\_流\_请求\_块结构传递**AVCSTRM\_打开**为宏的请求参数。 接下来，设置子单元驱动程序**AVCStreamContext**成员添加到**NULL**。 成功执行操作，此成员应包含有效的流上下文 （句柄），可在后续*avcstrm.sys*操作。 此成员不应修改之后直到流已关闭，通过[ **AVCSTRM\_关闭**](avcstrm-close.md)... 最后，将子单元驱动程序设置**OpenStruct**的成员**CommandData**描述要打开的流的并集。

若要发送此请求，子单元提交[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)与 IRP **IoControlCode** IRP 成员设置为[ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)并**Argument1** IRP 成员设置为AVC\_流\_请求\_描述发生的打开操作的块结构。

子单元驱动程序可能会以同步方式完成此命令。 挂起的操作中而不立即返回的结果*avcstrm.sys*。

此函数代码必须调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff554194)， [ **INIT\_AVCSTRM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560750)， [ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)， [ **IOCTL\_AVCSTRM\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560778)， [ **AVCSTRM\_打开\_结构**](https://msdn.microsoft.com/library/windows/hardware/ff554127)， [ **AVCSTRM\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)， [ **AVCSTRM\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff554114)， [ **AVCSTRM\_格式\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554117)

 

 





