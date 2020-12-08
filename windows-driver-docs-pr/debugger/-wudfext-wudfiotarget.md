---
title: wudfext.wudfiotarget
description: Wudfext. wudfiotarget 扩展显示有关 i/o 目标的信息，包括目标的状态和已发送请求的列表。
keywords:
- wudfext wudfiotarget Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfiotarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 370b65a5a1864e76167cf80bc6785110017a3521
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794057"
---
# <a name="wudfextwudfiotarget"></a>!wudfext.wudfiotarget


**！ Wudfext wudfiotarget** 扩展显示有关 i/o 目标的信息，包括目标的状态和已发送请求的列表。

```dbgcmd
!wudfext.wudfiotarget pWDFTarget TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______pWDFTarget______"></span><span id="_______pwdftarget______"></span><span id="_______PWDFTARGET______"></span>*pWDFTarget*   
指定要显示其相关信息的 **IWDFIoTarget** 接口的地址。 [**！ Wudfext wudfobject**](-wudfext-wudfobject.md) extension 命令确定 **IWDFIoTarget** 的地址。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span>*TypeName*   
可选。 指定接口的类型 (例如 **IWDFDevice**) 。 如果为 *TypeName* 提供了一个值，扩展将使用值作为该接口的类型。 如果将星号 (\*) 提供为 *typename*，或者省略 *typename* ，则扩展将尝试自动确定所提供的接口的类型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP （UMDF 版本1.7 及更高版本）</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

 

 





