---
title: EXT\_TDOP\_获取\_字段
description: EXT\_TDOP\_获取调试\_请求\_"字段" 子操作\_"\_" 类型\_"数据\_ANSI 请求操作" 返回表示给定结构成员的类型化数据说明。
ms.assetid: c91c0ecf-c093-4585-a6b5-6bda91899ec3
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
ms.openlocfilehash: a31a6261242ddb00639cf9bcac9489bed850431c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826461"
---
# <a name="ext_tdop_get_field"></a>EXT\_TDOP\_获取\_字段


EXT\_TDOP\_获取调试\_请求\_"字段" 子操作\_"扩展"\_"[**数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作" 返回表示的成员的类型化数据说明给定的结构。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_获取此子操作\_字段。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定一个[**调试\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)的实例，该实例描述需要其成员的结构。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收所请求成员的[**DEBUG\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)的实例。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定请求的成员的名称。 成员的名称是一个点分隔的路径，可以包含子成员（例如**mymember. mysubmember**。 此点分隔路径上的指针将自动取消引用。 但是，仍应在此处使用点运算符（ **.** ），而不是常规的 C 指针取消引用运算符（ **-&gt;** ）。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_GET\_字段是[**ext\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






