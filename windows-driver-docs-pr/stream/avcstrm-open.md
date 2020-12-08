---
title: AVCSTRM \_ 打开
description: AVCSTRM \_ 打开
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
ms.openlocfilehash: 83a92f4e434c6ed0487b41275d4a0e78a9253e72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788215"
---
# <a name="avcstrm_open"></a>AVCSTRM \_ 打开


## <span id="ddk_avcstrm_open_ks"></span><span id="DDK_AVCSTRM_OPEN_KS"></span>


**AVCSTRM \_ OPEN** 函数代码打开具有特定流格式的流。

### <a name="io-status-block"></a>I/o 状态块

如果成功， *avcstrm.sys* 将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

如果成功，将 \_ 返回状态 "成功" 和 " [**AVC \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)结构" 的 **AVCStreamContext** 成员中的流上下文。 此上下文随后用于其他 *avcstrm.sys* 请求。

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

此函数使用 AVC 流请求块结构中的 **CommandData** 联合的 **OpenStruct** 成员 \_ ，如下 \_ \_ 所示。

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

**标头：** 在 *avcstrm* 中声明。 包括 *avcstrm*。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC \_ 流 \_ 请求 \_ 块输入

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、Version 和 Function**  
使用 [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header) 宏初始化这些成员。 传递 **AVCSTRM \_** 在宏的请求参数中打开。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
指定 (处理) 的流上下文。 对于输入，此值应为 **NULL** ，如果 **AVCSTRM \_ 打开** 成功返回，则此成员包含用于后续 *avcstrm.sys* 操作的有效流上下文。

<span id="OpenStruct"></span><span id="openstruct"></span><span id="OPENSTRUCT"></span>**OpenStruct**  
指定要创建的 AV/C 流的说明。

[**AVCSTRM \_ 格式**](/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_format)枚举提供 *avcstrm.sys* 支持的 IEC 61883 规格)  (支持的 AV/C 流式处理格式列表，如 SDDV (61883-2) 和 MPEG2TS (61883-4) 。

为了建立同步连接，CIP 标头和子单元依赖参数是必需的，并且是在 [**AVCSTRM \_ 格式 \_ 信息**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info) 结构中定义的。

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

子单元驱动程序必须首先分配 IRP 和 [**AVC \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block) 结构。 接下来，它应使用 [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header) 宏来初始化 AVC \_ 流 \_ 请求 \_ 块结构，并 **将 \_ AVCSTRM** 作为 REQUEST 参数传递到宏。 接下来，子单位驱动程序将 **AVCStreamContext** 成员设置为 **NULL**。 成功操作时，此成员应包含有效的流上下文， (处理后续 *avcstrm.sys* 操作中使用的句柄) 。 在通过 [**AVCSTRM \_ CLOSE**](avcstrm-close.md)关闭流之前，不应修改此成员。 最后，子单位驱动程序设置描述要打开的流的 **CommandData** 联合的 **OpenStruct** 成员。

若要发送此请求，子组会 [**将 \_ irp \_ MJ \_ 内部设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md) irp，并将 irp 集的 **IoControlCode** 成员提交给 [**IOCTL \_ AVCSTRM \_ 类**](/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class) ，并将 irp 集的 **Argument1** 成员提交到 \_ \_ \_ 描述要发生的打开操作的 AVC 流请求块结构。

子单位驱动程序可能希望此命令同步完成。 结果会立即返回，而不会在 *avcstrm.sys* 中挂起操作。

必须在 IRQL = 被动级别调用此函数代码 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)， [**INIT \_ AVCSTRM \_ 标头**](/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)， [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)， [**IOCTL \_ AVCSTRM \_ 类**](/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)， [**AVCSTRM \_ 开放 \_ 结构**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_open_struct)， [**AVCSTRM \_ 函数**](/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)， [**AVCSTRM \_ 格式**](/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_format)， [**AVCSTRM \_ 格式 \_ 信息**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)

 

