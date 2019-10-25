---
title: AVCSTRM\_打开
description: AVCSTRM\_打开
ms.assetid: d352615b-8ab8-40ac-b165-479686abd587
keywords:
- AVCSTRM_OPEN 流媒体设备
topic_type:
- apiref
api_name:
- AVCSTRM_OPEN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2650840e7c6caa9c39b26507f40ac6b9f5c214
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845025"
---
# <a name="avcstrm_open"></a>AVCSTRM\_打开


## <span id="ddk_avcstrm_open_ks"></span><span id="DDK_AVCSTRM_OPEN_KS"></span>


**AVCSTRM\_打开**函数代码以特定流格式打开流。

### <a name="io-status-block"></a>I/O 状态块

如果成功， *avcstrm*会将**Irp&gt;IOSTATUS**设置为 STATUS，状态\_SUCCESS。

如果成功，将在[**AVC\_stream\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)结构的**AVCStreamContext**成员中返回状态\_"成功"。 此上下文随后用于其他*avcstrm*请求。

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

此函数使用 AVC\_流\_请求\_块结构中的**CommandData**联合的**OpenStruct**成员，如下所示。

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

**标头：** 在*avcstrm*中声明。 包括*avcstrm*。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_STREAM\_请求\_块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、Version 和 Function**  
使用[**INIT\_AVCSTRM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)宏来初始化这些成员。 传递**AVCSTRM\_** 在宏的请求参数中打开。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定流上下文（句柄）。 输入时这应为**NULL** ，并且如果**AVCSTRM\_OPEN**成功返回，则此成员包含用于后续*AVCSTRM*操作的有效流上下文。

<span id="OpenStruct"></span><span id="openstruct"></span><span id="OPENSTRUCT"></span>**OpenStruct**  
指定要创建的 AV/C 流的说明。

[**AVCSTRM\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_format)枚举提供*AVCSTRM*支持的 AV/C 流式处理格式（来自 IEC 61883 规范）的列表，例如 SDDV （61883-2）和 MPEG2TS （61883-4）。

为了建立同步连接，CIP 标头和子单元依赖参数是必需的，并在[**AVCSTRM\_格式\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)结构中定义。

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

子单位驱动程序必须先分配 IRP，并[ **\_流\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)结构。 接下来，它应使用[**INIT\_AVCSTRM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)宏来初始化 AVC\_STREAM\_请求\_块结构，将**AVCSTRM\_** 作为 request 参数传递到宏。 接下来，子单位驱动程序将**AVCStreamContext**成员设置为**NULL**。 成功操作时，此成员应包含在后续*avcstrm*操作中使用的有效流上下文（句柄）。 在通过 AVCSTRM 关闭流之前，不应修改此成员， [ **\_CLOSE**](avcstrm-close.md)。 最后，子单位驱动程序设置描述要打开的流的**CommandData**联合的**OpenStruct**成员。

若要发送此请求，子组会将[**irp\_MJ 提交\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)irp，并将 irp 集的**IoControlCode**成员设置为[**IOCTL\_AVCSTRM\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)和**Argument1**IRP 的成员设置为 AVC\_STREAM\_请求\_块结构，描述要发生的打开操作。

子单位驱动程序可能希望此命令同步完成。 结果会立即返回，而不会在*avcstrm*中运行挂起的操作。

必须在 IRQL = 被动\_级别调用此函数代码。

### <a name="see-also"></a>另请参阅

[**AVC\_STREAM\_请求\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)， [**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)， [**IRP\_MJ\_内部\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)， [**IOCTL\_AVCSTRM\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)， [**AVCSTRM\_打开\_STRUCT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_open_struct)， [**AVCSTRM\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function) [**AVCSTRM\_FORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_format)， [**AVCSTRM\_格式\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)

 

 





