---
title: EXT \_ TDOP \_ GET \_ TYPE \_ SIZE
description: "\"调试请求\" 的 \"扩展 \\_ TDOP \\_ 获取 \\_ 类型 \\_ 大小\" 子操作 \" \\_ Ext 类型 \\_ \\_ 化 \\_ 数据 \\_ ANSI 请求\" 操作返回指定类型化数据的大小。"
keywords:
- EXT_TDOP_GET_TYPE_SIZE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_SIZE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ad8df899fcede66947d3e77c50d6078abf03e8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814573"
---
# <a name="ext_tdop_get_type_size"></a>EXT \_ TDOP \_ GET \_ TYPE \_ SIZE


"调试请求" 的 "扩展 \_ TDOP \_ 获取 \_ 类型 \_ 大小" 子操作 " [**ext 类型 \_ \_ \_ 化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md) " 操作返回指定类型化数据的大小。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ 获取 \_ \_ 此子操作的类型大小。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其大小的类型化数据。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
接收类型化数据的大小（以字节为单位）。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ GET \_ TYPE \_ SIZE 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

