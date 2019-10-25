---
title: EXT\_TDOP\_获取\_类型\_名称
description: EXT\_TDOP\_获取调试\_请求\_类型\_名称子操作\_EXT\_类型\_数据\_ANSI 请求操作返回指定类型化数据的类型名称。
ms.assetid: ce896ded-a49e-4f89-969e-6d464e583ca8
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
ms.openlocfilehash: e0db3ddb92be6a3c42334b7748a63c6d45fb9391
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826438"
---
# <a name="ext_tdop_get_type_name"></a>EXT\_TDOP\_获取\_类型\_名称


EXT\_TDOP\_获取调试\_请求\_类型\_名称子操作[ **\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回指定类型化的类型名称数据.

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_获取此子操作\_类型\_名称。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其类型名称的类型化数据。

<span id="StrBufferIndex"></span><span id="strbufferindex"></span><span id="STRBUFFERINDEX"></span>**StrBufferIndex**  
接收类型名称。

<span id="StrBufferChars"></span><span id="strbufferchars"></span><span id="STRBUFFERCHARS"></span>**StrBufferChars**  
指定 ANSI 字符串缓冲区**StrBufferIndex**的大小（以字符为字符）。

<span id="StrCharsNeeded"></span><span id="strcharsneeded"></span><span id="STRCHARSNEEDED"></span>**StrCharsNeeded**  
接收类型名称的大小（以字符为形式）。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_GET\_类型\_NAME 是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






