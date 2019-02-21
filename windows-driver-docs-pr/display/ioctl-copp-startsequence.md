---
title: IOCTL\_COPP\_StartSequence 控制代码
description: 将当前的视频会话设置为受保护模式。
ms.assetid: a28e22d0-b54d-45d2-b32c-b0d96960a8a2
keywords:
- IOCTL_COPP_StartSequence 控制代码的显示设备
topic_type:
- apiref
api_name:
- IOCTL_COPP_StartSequence
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 39a111f0c0de781eeb61c2535a9724693dcfc722
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544938"
---
# <a name="ioctlcoppstartsequence-control-code"></a>IOCTL\_COPP\_StartSequence 控制代码


将当前的视频会话设置为受保护模式。

## <span id="ddk_ioctl_copp_startsequence_gg"></span><span id="DDK_IOCTL_COPP_STARTSEQUENCE_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>输入的参数

[**视频\_请求\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff570547) (VRP) **InputBuffer**包含从显示器驱动程序传递的信息。 例如，显示器驱动程序，可以将指针传递到 COPP\_IO\_InputBuffer 结构定义，如下所示：

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**成员将指向对设置为受保护模式的 COPP DirectX VA 设备对象的指针。 **InputBuffer**成员设置为指向的指针[ **DXVA\_COPPSignature** ](https://msdn.microsoft.com/library/windows/hardware/ff563150)启动受保护的会话的结构。 **Phr**成员应设置为从返回的值[ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421)函数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>输出参数

无

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/O 状态块

微型端口驱动程序不会设置**信息**的成员[**状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff569732)结构。

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
<td align="left"><p>本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[*COPPSequenceStart*](https://msdn.microsoft.com/library/windows/hardware/ff540421)

[**DXVA\_COPPSignature**](https://msdn.microsoft.com/library/windows/hardware/ff563150)

 

 






