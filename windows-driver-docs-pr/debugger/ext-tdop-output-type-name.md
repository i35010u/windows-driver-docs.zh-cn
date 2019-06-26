---
title: EXT\_TDOP\_输出\_类型\_名称
description: EXT\_TDOP\_输出\_类型\_NAME 子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作打印指定的类型化数据的类型名称。
ms.assetid: eb0a9026-92fd-4b3e-b513-b691221b3196
keywords:
- EXT_TDOP_OUTPUT_TYPE_NAME Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11474fed4e918f34d393dee8f2362da59e2cd44a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366858"
---
# <a name="exttdopoutputtypename"></a>EXT\_TDOP\_输出\_类型\_名称


EXT\_TDOP\_输出\_类型\_名称的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作输出指定的类型化数据的类型名称。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_输出\_类型\_此子操作的名称。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其类型名称的类型化的数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

类型名称被发送到调试器引擎[输出回调](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)。

EXT\_TDOP\_输出\_类型\_名称是中的值[ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**请求**](request.md)

 

 






