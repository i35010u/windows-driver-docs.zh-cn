---
title: IOCTL \_ COPP \_ 状态控制代码
description: 返回受保护视频会话的状态。
ms.assetid: 58c841f6-0bc8-4c21-9c0e-fd409817ec91
keywords:
- IOCTL_COPP_Status 控制代码显示设备
topic_type:
- apiref
api_name:
- IOCTL_COPP_Status
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: af19e9cfa0b44b36f6214bc2ba27bb29d34bb448
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063900"
---
# <a name="ioctl_copp_status-control-code"></a>IOCTL \_ COPP \_ 状态控制代码


返回受保护视频会话的状态。

## <span id="ddk_ioctl_copp_status_gg"></span><span id="DDK_IOCTL_COPP_STATUS_GG"></span>


### <a name="span-idinput_parametersspanspan-idinput_parametersspanspan-idinput_parametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>输入参数

[**视频 \_ 请求 \_ 数据包**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) (VRP) **InputBuffer**包含从显示驱动程序传递的信息。 例如，显示驱动程序可以将指针传递给 \_ 定义为的 COPP IO \_ InputBuffer 结构，如下所示：

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**成员指向 COPP DirectX VA 设备对象的指针，该对象的状态为 "已检索"。 **InputBuffer**成员设置为指向[**DXVA \_ COPPStatusInput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)结构的指针，该结构包含有关 COPP 状态请求的信息。 应将 **phr** 成员设置为从 [*COPPQueryStatus*](./coppquerystatus.md) 函数返回的值。

### <a name="span-idoutput_parametersspanspan-idoutput_parametersspanspan-idoutput_parametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>输出参数

微型端口驱动程序返回指向 VRP **OutputBuffer**中的[**DXVA \_ COPPStatusOutput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)结构的指针。 DXVA \_ COPPStatusOutput 结构包含状态。

### <a name="span-idi_o_status_blockspanspan-idi_o_status_blockspanspan-idi_o_status_blockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/o 状态块

微型端口驱动程序将[**状态 \_ 块**](/windows-hardware/drivers/ddi/video/ns-video-_status_block)结构的**信息**成员设置为 sizeof (DXVA \_ COPPStatusOutput) 。

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


[*COPPQueryStatus*](./coppquerystatus.md)

[**DXVA \_ COPPStatusInput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)

[**DXVA \_ COPPStatusOutput**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)

 

