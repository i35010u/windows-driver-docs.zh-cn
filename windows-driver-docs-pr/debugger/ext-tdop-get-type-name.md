---
title: EXT \_ TDOP \_ GET \_ TYPE \_ NAME
description: '\_调试请求的 ext TDOP \_ GET \_ 类型 \_ 名称子操作 ext 类型 \_ \_ 化的 \_ \_ 数据 \_ ANSI 请求操作返回指定类型化数据的类型名称。'
keywords:
- EXT_TDOP_GET_TYPE_NAME Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f4517d1ad476932739a703797cb24f7858a3617
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839949"
---
# <a name="ext_tdop_get_type_name"></a>EXT \_ TDOP \_ GET \_ TYPE \_ NAME


\_调试请求的 ext TDOP \_ GET \_ 类型 \_ 名称子操作 [**ext 类型 \_ 化 \_ 的 \_ \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回指定类型化数据的类型名称。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ 获取 \_ \_ 此子操作的类型名称。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其类型名称的类型化数据。

<span id="StrBufferIndex"></span><span id="strbufferindex"></span><span id="STRBUFFERINDEX"></span>**StrBufferIndex**  
接收类型名称。

<span id="StrBufferChars"></span><span id="strbufferchars"></span><span id="STRBUFFERCHARS"></span>**StrBufferChars**  
指定 ANSI 字符串缓冲区 **StrBufferIndex** 的大小（以字符为字符）。

<span id="StrCharsNeeded"></span><span id="strcharsneeded"></span><span id="STRCHARSNEEDED"></span>**StrCharsNeeded**  
接收类型名称的大小（以字符为形式）。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ GET \_ TYPE \_ NAME 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

