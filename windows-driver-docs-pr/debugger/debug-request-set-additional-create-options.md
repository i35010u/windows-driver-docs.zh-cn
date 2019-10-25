---
title: 调试\_请求\_集\_其他\_创建\_选项
description: 调试\_请求\_集\_其他\_创建\_选项
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
ms.openlocfilehash: 8818fecff5db9e900d14984477637afb2b778ca9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837790"
---
# <a name="debug_request_set_additional_create_options"></a>调试\_请求\_集\_其他\_创建\_选项


调试\_请求\_集\_其他\_CREATE\_OPTIONS[**请求**](request.md)操作设置默认进程创建选项。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新的默认进程创建选项。 进程创建选项的类型为[**DEBUG\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
不使用。

<a name="remarks"></a>备注
-------

默认进程创建选项用于方法[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)和[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach) ，与[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)和[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)不同，它们不指定进程创建选项的全部范围。

[**调试\_CREATE\_PROCESS\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)结构的 " **CreateFlags** " 字段不用作默认结构，因为所有进程创建操作都提供此信息。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**需要**](request.md)

[**调试\_请求\_获取\_其他\_创建\_选项**](debug-request-get-additional-create-options.md)

[**调试\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

 






