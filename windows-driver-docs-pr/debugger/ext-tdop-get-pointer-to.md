---
title: EXT \_ TDOP \_ GET \_ 指针 \_
description: EXT \_ TDOP \_ GET \_ 指针 \_ 指向调试请求的子操作 \_ \_ Ext \_ 类型化的 \_ 数据 \_ ANSI 请求操作返回一个新的类型化数据说明，该说明表示指向指定类型化数据的指针。
ms.assetid: 05db8e07-b94f-4cf3-b01b-a918b737ecf4
keywords:
- EXT_TDOP_GET_POINTER_TO Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_POINTER_TO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe2a18d13078fb282fdc2166af0a646f11b55f2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212989"
---
# <a name="ext_tdop_get_pointer_to"></a>EXT \_ TDOP \_ GET \_ 指针 \_


EXT \_ TDOP \_ GET \_ 指针 \_ 指向调试请求的子操作 [** \_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md) 操作返回一个新的类型化数据说明，该说明表示指向指定类型化数据的指针。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ 获取 \_ 指向 \_ 此子操作的指针。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定指针返回到的原始类型化数据说明。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收一个类型化的数据说明，该说明表示指向由 **InData**指定的类型化数据的指针。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ GET \_ 指针 \_ 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

