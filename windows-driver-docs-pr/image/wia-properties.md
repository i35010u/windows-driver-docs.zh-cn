---
title: WIA 属性
description: WIA 属性
ms.assetid: 3b9d4d90-775b-450e-b5d1-646ea45253d7
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 192097f625abf4c76fcfd5ff0559449858e55199
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223572"
---
# <a name="wia-properties"></a>WIA 属性

本部分包含 WIA 属性及其属性。

这些属性的参考主题列出了以下属性：属性类型、有效值和访问权限。

## <a name="property-types"></a>属性类型

WIA 中使用以下类型来指示属性的数据类型：

**VT \_ BSTR**

Unicode 字符（宽字符字符串）的字符串。

**VT \_ I4**

4字节整数。

**VT \_ R4**

4字节实数（C **float**）。

**VT \_ UI2**

2 字节无符号整数。

**VT \_ 矢量**

特定类型的元素的数组。 如果通过使用 OR 运算符将其他属性类型与 VT \_ 矢量结合使用，则生成的值是由 DWORD 计算的元素组成的计数数组，后跟指向数组中第一个元素的指针。 例如，VT \_ UI2 |VT \_ VECTOR 具有 DWORD 元素计数，后跟一个指向2字节无符号整数元素数组的指针。

## <a name="valid-values"></a>有效值

以下类型指示属性是否作为单个值、值的范围、值列表或标志存在：

**WIA \_ " \_ 无"**

属性包含单个值。

**WIA 的 " \_ \_ 范围"**

属性包含一个值范围，包括最小值、最大值、名义值和增量。

**WIA \_ \_ 列表**

属性包含值列表。

**WIA \_ \_ 标识符标志**

属性包含一个标志。

## <a name="access-rights"></a>访问权限

以下列表描述了属性的可能访问权限：

**只读**

该驱动程序具有只读访问权限。

**读/写** 

驱动程序具有读取和写入访问权限。

## <a name="remarks"></a>备注

前面的列表仅描述了在此部分包含的 WIA 属性中使用的那些类型。 

有关这些属性类型和其他属性类型的详细信息，请参阅[**WIA \_ 属性 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)。

Windows SDK 包含有关[WIA \_ 原始 \_ 标头](https://docs.microsoft.com/windows/win32/wia/-wia-wia-raw-header)结构的信息。

它还包含有关 WIA 事件 \_ \_ XXX 和 wia \_ CMD \_ XXX 常量的信息，请参阅[wia 事件标识符](https://docs.microsoft.com/windows/win32/wia/-wia-wia-event-identifiers)主题。
