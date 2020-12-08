---
title: INF DelProperty 指令
description: DelProperty 引用了用于删除设备实例、设备安装程序类、设备接口类或设备接口的设备属性的 INF 文件部分。
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
ms.openlocfilehash: d2f0f0fd4d94776895b9aa12fcd9d2b6b9dc9ec5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838469"
---
# <a name="inf-delproperty-directive"></a>INF DelProperty 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**DelProperty** 指令将引用一个或多个用于删除设备实例、[设备安装程序类](./overview-of-device-setup-classes.md)、[设备接口类](./overview-of-device-interface-classes.md)或设备接口的 [设备属性](device-properties.md)的 INF 文件部分。

```inf
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

可以在上述正式语法语句中所示的任何节下指定 **DelProperty** 指令。

**DelProperty** 指令引用的 *del 属性部分* 具有以下格式：

```inf
[del-property-section]
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
...
```

*Del-属性部分* 可以有任意数量的 *属性名称* 条目或 *属性 guid* 条目，每个条目都在单独的行上。

## <a name="entries"></a>项


<a href="" id="property-name"></a>*属性-名称*  
表示设备实例 [驱动程序包](driver-packages.md) 属性的属性名称之一。 支持的属性名称与 [**INF AddProperty 指令**](inf-addproperty-directive.md)的 *属性名称* 条目中描述的属性名称相同。

<a href="" id="property-category-guid"></a>*属性类别-guid*  
标识属性类别的 GUID 值。 GUID 值可以是系统定义的 GUID，用于标识系统定义的属性类别或标识自定义属性类别的自定义 GUID。 支持的 GUID 值与 INF [**AddProperty**](inf-addproperty-directive.md)指令的 *属性类别 guid* 条目描述的值相同。

<a href="" id="property-pid"></a>*属性-pid*  
一个属性标识符，指示属性类别内的特定属性，该属性由 *属性类别 guid* 值指示。 由于内部系统原因，属性标识符必须大于或等于2。

<a href="" id="flags"></a>*随意*  
用于控制删除操作的可选十六进制标志值。 支持的唯一标志值如下所示：

<a href="" id="0x00000001--flg-delproperty-multi-sz-delstring-"></a>**0x00000001** (FLG_DELPROPERTY_MULTI_SZ_DELSTRING)   
如果属性数据类型为 [**DEVPROP_TYPE_STRING_LIST**](./devprop-type-string-list.md)，则操作将删除所有字符串，其中包含与值输入值提供的字符串匹配的现有字符串列表。 在提供的字符串与字符串列表中的现有字符串之间的比较中，不考虑字符的大小写。

<a href="" id="value"></a>value  
如果属性数据类型为 DEVPROP_TYPE_STRING_LIST 并且标志条目为 **0x00000001**，则 *值* 输入值将提供删除操作用于在现有字符串列表中搜索匹配字符串的字符串，如果找到匹配的字符串，则删除操作将从现有字符串列表中删除匹配的字符串。

<a name="remarks"></a>备注
-------

通常，不应使用 INF 文件来删除可能由系统组件或其他 INF 文件设置的设备属性。 **DelProperty** 指令的主要用途是在 INF 文件中使用，该文件将更新以前的设备安装，不再需要为先前设备安装设置的属性。

在 INF 文件中， *del-property 节* 名称必须是唯一的，但在同一 INF 文件中，可以通过多个 **DelProperty** 指令引用部分名称。 节名称必须遵循用于定义用于 [INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中所述的部分名称的常规规则。

有关如何使用 **DelProperty** 指令的详细信息，请参阅 [使用 inf ADDPROPERTY 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a name="examples"></a>示例
--------

以下 "删除属性" 部分的示例包括两个行条目：第一行条目包含一个用于删除 **DeviceModel** 属性的 *属性名称* 条目值，第二个行条目从其数据类型为 DEVPROP_TYPE_STRING_LIST 的自定义设备属性值中删除字符串 "DeleteThisString"。 在第二行中， *属性-category-guid* 条目值为 "c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"， *属性标识符* 条目值为 "2"， *标志* 条目值为 "0x00000001"

```inf
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

## <a name="see-also"></a>请参阅


[**AddProperty**](inf-addproperty-directive.md)

 

