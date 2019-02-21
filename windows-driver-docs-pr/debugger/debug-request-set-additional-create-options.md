---
title: DEBUG\_REQUEST\_SET\_ADDITIONAL\_CREATE\_OPTIONS
description: DEBUG\_REQUEST\_SET\_ADDITIONAL\_CREATE\_OPTIONS
ms.assetid: e80f8575-b7f9-466a-8087-b3cb103503f7
keywords:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a443041865d023db1669747a1b03a4bd9696bc1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519368"
---
# <a name="debugrequestsetadditionalcreateoptions"></a>DEBUG\_REQUEST\_SET\_ADDITIONAL\_CREATE\_OPTIONS


调试\_请求\_设置\_其他\_创建\_选项[**请求**](request.md)操作设置默认进程创建选项。

**参数**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新的默认进程创建选项。 进程创建选项的类型是[**调试\_创建\_进程\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541464)。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
不使用。

<a name="remarks"></a>备注
-------

方法使用的默认进程创建选项[ **CreateProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff539321)并[ **CreateProcessAndAttach** ](https://msdn.microsoft.com/library/windows/hardware/ff540048)这与不同[**CreateProcess2** ](https://msdn.microsoft.com/library/windows/hardware/ff539323)并[ **CreateProcessAndAttach2**](https://msdn.microsoft.com/library/windows/hardware/ff540055)，未指定进程创建选项的完整范围。

**CreateFlags**字段[**调试\_创建\_过程\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541464)结构不使用默认情况下，因为所有进程创建操作提供此信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

[**DEBUG\_REQUEST\_GET\_ADDITIONAL\_CREATE\_OPTIONS**](debug-request-get-additional-create-options.md)

[**调试\_创建\_进程\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541464)

[**CreateProcess**](https://msdn.microsoft.com/library/windows/hardware/ff539321)

[**CreateProcessAndAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540048)

 

 






