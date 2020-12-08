---
title: EXT \_ TDOP \_ GET \_ 字段
description: '\_调试请求的 ext TDOP \_ GET \_ FIELD sub 操作 \_ \_ Ext \_ 类型化 \_ 数据 \_ ANSI 请求操作返回表示给定结构成员的类型化数据说明。'
keywords:
- EXT_TDOP_GET_FIELD Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 927e5c671bb79ca5baf82c8dad87994a10a70659
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814575"
---
# <a name="ext_tdop_get_field"></a>EXT \_ TDOP \_ GET \_ 字段


\_调试请求的 ext TDOP \_ GET \_ FIELD sub 操作 [**\_ \_ ext \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回表示给定结构成员的类型化数据说明。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_对于此子操作，设置为 EXT TDOP \_ GET \_ FIELD。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 的实例，该实例描述需要其成员的结构。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收所请求成员的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 的实例。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定请求的成员的名称。 成员的名称是一个点分隔的路径，可以包含子成员（例如 **mymember. mysubmember**。 此点分隔路径上的指针将自动取消引用。 但是，点 **运算符 (，** 此处仍应使用) ，而不是常规的 C 指针取消引用运算符 (**-&gt;**) 。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ GET \_ FIELD 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

