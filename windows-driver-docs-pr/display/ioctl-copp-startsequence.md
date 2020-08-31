---
title: IOCTL \_ COPP \_ StartSequence 控制代码
description: 将当前视频会话设置为受保护模式。
ms.assetid: a28e22d0-b54d-45d2-b32c-b0d96960a8a2
keywords:
- IOCTL_COPP_StartSequence 控制代码显示设备
topic_type:
- apiref
api_name:
- IOCTL_COPP_StartSequence
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6403d66621508d773b32f536556161c9ccd6703b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063904"
---
# <a name="ioctl_copp_startsequence-control-code"></a>IOCTL \_ COPP \_ StartSequence 控制代码


将当前视频会话设置为受保护模式。

## <span id="ddk_ioctl_copp_startsequence_gg"></span><span id="DDK_IOCTL_COPP_STARTSEQUENCE_GG"></span>


### <a name="span-idinput_parametersspanspan-idinput_parametersspanspan-idinput_parametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>输入参数

[**视频 \_ 请求 \_ 数据包**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) (VRP) **InputBuffer**包含从显示驱动程序传递的信息。 例如，显示驱动程序可以将指针传递给 \_ 定义为的 COPP IO \_ InputBuffer 结构，如下所示：

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**成员指向设置为 "保护模式" 的 COPP DirectX VA 设备对象的指针。 **InputBuffer**成员设置为一个指向[**DXVA \_ COPPSignature**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsignature)结构的指针，该结构启动受保护的会话。 应将 **phr** 成员设置为从 [*COPPSequenceStart*](./coppsequencestart.md) 函数返回的值。

### <a name="span-idoutput_parametersspanspan-idoutput_parametersspanspan-idoutput_parametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>输出参数

无

### <a name="span-idi_o_status_blockspanspan-idi_o_status_blockspanspan-idi_o_status_blockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/o 状态块

微型端口驱动程序不会设置[**状态 \_ 块**](/windows-hardware/drivers/ddi/video/ns-video-_status_block)结构的**信息**成员。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[*COPPSequenceStart*](./coppsequencestart.md)

[**DXVA \_ COPPSignature**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsignature)

 

