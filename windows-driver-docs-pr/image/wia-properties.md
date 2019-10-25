---
title: WIA 属性
description: WIA 属性
ms.assetid: 3b9d4d90-775b-450e-b5d1-646ea45253d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4c9a443c367cdb6fef38a28c4955fe77249c17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840673"
---
# <a name="wia-properties"></a>WIA 属性


## <span id="ddk_wia_properties_si"></span><span id="DDK_WIA_PROPERTIES_SI"></span>


本部分包含 WIA 属性及其属性。

这些属性的参考主题列出了以下属性：属性类型、有效值和访问权限。

### <a name="span-idproperty_typesspanspan-idproperty_typesspanproperty-types"></a><span id="property_types"></span><span id="PROPERTY_TYPES"></span>属性类型

WIA 中使用以下类型来指示属性的数据类型：

<span id="VT_BSTR"></span><span id="vt_bstr"></span>VT\_BSTR  
Unicode 字符（宽字符字符串）的字符串。

<span id="VT_I4"></span><span id="vt_i4"></span>VT\_I4  
4字节整数。

<span id="VT_R4"></span><span id="vt_r4"></span>VT\_R4  
4字节实数（C **float**）。

<span id="VT_UI2"></span><span id="vt_ui2"></span>VT\_UI2  
2字节无符号整数。

<span id="VT_VECTOR"></span><span id="vt_vector"></span>VT\_向量  
特定类型的元素的数组。 如果通过使用 OR 运算符将其他属性类型与 VT\_VECTOR 结合使用，则生成的值是由 DWORD 值元素组成的计数数组，后跟指向数组中第一个元素的指针。 例如，VT\_UI2 |VT\_向量具有 DWORD 元素计数，后跟一个指向2字节无符号整数元素数组的指针。

### <a name="span-idvalid_valuesspanspan-idvalid_valuesspanvalid-values"></a><span id="valid_values"></span><span id="VALID_VALUES"></span>有效值

以下类型指示属性是否作为单个值、值的范围、值列表或标志存在：

<span id="WIA_PROP_NONE"></span><span id="wia_prop_none"></span>WIA\_\_NONE  
属性包含单个值。

<span id="WIA_PROP_RANGE"></span><span id="wia_prop_range"></span>WIA\_\_范围  
属性包含一个值范围，包括最小值、最大值、名义值和增量。

<span id="WIA_PROP_LIST"></span><span id="wia_prop_list"></span>WIA\_\_列表  
属性包含值列表。

<span id="WIA_PROP_FLAG"></span><span id="wia_prop_flag"></span>WIA\_\_标志  
属性包含一个标志。

### <a name="span-idaccess_rightsspanspan-idaccess_rightsspanaccess-rights"></a><span id="access_rights"></span><span id="ACCESS_RIGHTS"></span>访问权限

以下列表描述了属性的可能访问权限：

<span id="Read-only"></span><span id="read-only"></span><span id="READ-ONLY"></span>只读  
该驱动程序具有只读访问权限。

<span id="Read_write"></span><span id="read_write"></span><span id="READ_WRITE"></span>读/写  
驱动程序具有读取和写入访问权限。

前面的列表仅描述了在此部分包含的 WIA 属性中使用的那些类型。 有关这些属性类型和其他属性类型的详细信息，请参阅[**WIA\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)。

Windows SDK 包含有关[WIA\_RAW\_页眉](https://go.microsoft.com/fwlink/p/?linkid=153316)结构的信息。 它还包含有关 WIA[事件标识符](https://go.microsoft.com/fwlink/p/?linkid=153318)主题中讨论的 WIA\_事件\_XXX 和 wia\_\_命令的信息。

 

 





