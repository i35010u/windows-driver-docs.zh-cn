---
title: INF DelProperty 指令
description: DelProperty 引用删除的设备实例、 设备安装程序类、 设备接口类或设备接口设备属性的 INF 文件部分。
ms.assetid: fff227de-1664-4c9b-8709-1a8e1966bd79
keywords:
- INF DelProperty 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DelProperty Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af3fee05f59822117c7416135f2dada6eb1dd17
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358814"
---
# <a name="inf-delproperty-directive"></a>INF DelProperty 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**DelProperty**指令引用删除的一个或多个 INF 文件节[设备属性](device-properties.md)对于设备实例，[设备安装程序类](device-setup-classes.md)、 [设备接口类](device-interface-classes.md)，或设备接口。

```ini
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm] |  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64] |  (Windows 10 and later versions of Windows)

[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] |  (Windows XP and later versions of Windows)
[interface-install-section.ntamd64] |  (Windows XP and later versions of Windows)
[interface-install-section.ntarm] |  (Windows 8 and later versions of Windows)
[interface-install-section.ntarm64] |  (Windows 10 and later versions of Windows)


[add-interface-section] 
 
DelProperty=del-property-section[,del-property-section]...  (Windows Vista and later versions of Windows)
```

一个**DelProperty**指令可以指定任何正式语法语句更高版本中所示的部分下。

一个*del 属性部分*引用**DelProperty**指令具有以下格式：

```ini
[del-property-section]
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
...
```

一个*del 属性部分*可以有任意数量的*属性名称*条目或*属性 guid*条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="property-name"></a>*property-name*  
其中一个属性名称表示设备实例[驱动程序包](driver-packages.md)属性。 支持的属性名称将与那些所述的相同*属性名称*的条目[ **INF AddProperty 指令**](inf-addproperty-directive.md)。

<a href="" id="property-category-guid"></a>*property-category-guid*  
一个 GUID 值，该值标识属性类别。 GUID 值可以是一个系统定义的 GUID，标识系统定义的属性类别或标识自定义属性类别的自定义 GUID。 支持的 GUID 值都是与所介绍的相同*属性类别 guid* INF 条目[ **AddProperty** ](inf-addproperty-directive.md)指令。

<a href="" id="property-pid"></a>*property-pid*  
指示所指示的属性类别中的特定属性的属性标识符*属性类别 guid*值。 内部系统方面的考虑，属性标识符必须大于或等于 2。

<a href="" id="flags"></a>*flags*  
一个可选的十六进制标志值，控制删除操作。 唯一支持的标志值如下所示：

<a href="" id="0x00000001--flg-delproperty-multi-sz-delstring-"></a>**0x00000001** (FLG_DELPROPERTY_MULTI_SZ_DELSTRING)  
如果属性数据类型为[ **DEVPROP_TYPE_STRING_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff543614)，该操作将删除与现有的字符串列表与提供的值条目值的字符串匹配的所有字符串。 所提供的字符串与字符串列表中的现有字符串之间的比较中不考虑的字符大小写。

<a href="" id="value"></a>*value*  
如果属性数据类型为 DEVPROP_TYPE_STRING_LIST 且标志条目**0x00000001**，则*值*条目值提供了删除操作用于匹配的字符串中的搜索字符串现有的字符串列表，并且如果找到匹配的字符串，则删除操作从现有字符串列表中删除匹配的字符串。

<a name="remarks"></a>备注
-------

一般情况下，一个 INF 文件，不应使用要删除的系统组件或另一个 INF 文件可能设置的设备属性。 主要目的**DelProperty**指令是在以前的设备安装更新的 INF 文件中使用和不再需要为以前的设备安装设置的属性。

一个*del 属性部分*名称中必须是唯一的 INF 文件，但可由多个引用的节名称**DelProperty**指令相同的 INF 文件中。 节名称必须遵循的一般规则用于定义中所述的节名称[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

有关如何使用详细信息**DelProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a name="examples"></a>示例
--------

删除属性部分的下面的示例包含两个行项： 第一个行条目包含*属性名称*删除的项值**DeviceModel**属性，并在第二个行条目的数据类型是 DEVPROP_TYPE_STRING_LIST 的自定义设备属性值中删除"DeleteThisString"的字符串。 在第二个行中，*属性类别 guid*条目值是"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e，"*属性标识符*条目值为"2，"和*标志*条目值是"0x00000001，"

```ini
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

## <a name="see-also"></a>请参阅


[**AddProperty**](inf-addproperty-directive.md)

 

 






