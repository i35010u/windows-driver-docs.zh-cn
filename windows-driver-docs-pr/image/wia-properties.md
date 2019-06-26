---
title: WIA 属性
description: WIA 属性
ms.assetid: 3b9d4d90-775b-450e-b5d1-646ea45253d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e41698b5b24bf979be6437c4629656e7980fdeb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355166"
---
# <a name="wia-properties"></a>WIA 属性


## <span id="ddk_wia_properties_si"></span><span id="DDK_WIA_PROPERTIES_SI"></span>


本部分包含的所有 WIA 属性和其属性。

这些属性的参考主题列出了以下属性： 属性类型、 有效的值和访问权限。

### <a name="span-idpropertytypesspanspan-idpropertytypesspanproperty-types"></a><span id="property_types"></span><span id="PROPERTY_TYPES"></span>属性类型

以下类型使用 WIA 以指示属性的数据类型：

<span id="VT_BSTR"></span><span id="vt_bstr"></span>VT\_BSTR  
一个 Unicode 字符 （宽字符字符串） 的字符串。

<span id="VT_I4"></span><span id="vt_i4"></span>VT\_I4  
一个 4 字节整数。

<span id="VT_R4"></span><span id="vt_r4"></span>VT\_R4  
4 字节实数 (C **float**)。

<span id="VT_UI2"></span><span id="vt_ui2"></span>VT\_UI2  
2 字节的无符号的整数。

<span id="VT_VECTOR"></span><span id="vt_vector"></span>VT\_向量  
特定类型的元素的数组。 如果另一种属性类型结合了 VT\_使用 OR 运算符，生成的值的向量是包含 DWORD 数量的元素，第一个后跟一个指针，一个计数的数组的数组中的元素。 例如，VT\_UI2 |VT\_向量的 DWORD 元素计数，跟一个 2 字节无符号的整数元素的数组的指针。

### <a name="span-idvalidvaluesspanspan-idvalidvaluesspanvalid-values"></a><span id="valid_values"></span><span id="VALID_VALUES"></span>有效的值

以下类型指示属性是否存在作为单个值，一定范围的值、 一系列值或一个标志：

<span id="WIA_PROP_NONE"></span><span id="wia_prop_none"></span>WIA\_PROP\_NONE  
属性包含单个值。

<span id="WIA_PROP_RANGE"></span><span id="wia_prop_range"></span>WIA\_PROP\_RANGE  
属性包含某个范围的值，包括最小值、 最大值、 标称值和增量。

<span id="WIA_PROP_LIST"></span><span id="wia_prop_list"></span>WIA\_PROP\_LIST  
属性包含值的列表。

<span id="WIA_PROP_FLAG"></span><span id="wia_prop_flag"></span>WIA\_PROP\_FLAG  
属性包含的标志。

### <a name="span-idaccessrightsspanspan-idaccessrightsspanaccess-rights"></a><span id="access_rights"></span><span id="ACCESS_RIGHTS"></span>访问权限

以下列表描述了一个属性的可能的访问权限：

<span id="Read-only"></span><span id="read-only"></span><span id="READ-ONLY"></span>只读的  
该驱动程序具有只读访问权限。

<span id="Read_write"></span><span id="read_write"></span><span id="READ_WRITE"></span>Read/write  
该驱动程序都具有读取和写入访问权限。

前面的列表介绍了在本部分包含的 WIA 属性中使用的那些类型。 有关这些和其他属性类型的详细信息，请参阅[ **WIA\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)。

Windows SDK 的信息包含有关[WIA\_RAW\_标头](https://go.microsoft.com/fwlink/p/?linkid=153316)结构。 它还包含了解 WIA\_事件\_XXX 和 WIA\_CMD\_中所述的 XXX 常量[WIA 事件标识符](https://go.microsoft.com/fwlink/p/?linkid=153318)主题。

 

 





