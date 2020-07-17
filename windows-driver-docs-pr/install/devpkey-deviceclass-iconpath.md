---
title: DEVPKEY_DeviceClass_IconPath
description: DEVPKEY_DeviceClass_IconPath
ms.assetid: c81ea18d-dd21-4b5e-8aba-52f7ad6931bf
keywords:
- DEVPKEY_DeviceClass_IconPath 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_IconPath
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d0e01602116fedd2718b43e8adaeb9412a65a5f4
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418536"
---
# <a name="devpkey_deviceclass_iconpath"></a>DEVPKEY_DeviceClass_IconPath


DEVPKEY_DeviceClass_IconPath 设备属性表示[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)的图标列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_IconPath</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值名称</strong></p></td>
<td align="left"><p><strong>IconPath</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以调用[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)或[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)来检索 DEVPKEY_DeviceClass_IconPath 的值。

DEVPKEY_DeviceClass_IconPath 值是由 Windows shell 使用的格式的图标资源说明符的[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)类型的列表。 图标资源说明符的格式为 "*可执行文件-路径*，*资源标识符*"，其中*可执行文件路径*包含计算机上文件的完全限定路径，该文件包含图标资源和*资源标识符*，指定用于标识资源的整数。 例如，图标资源说明符 "% SystemRoot% \\ system32 \\DLL1.dll，-12" 包含可执行文件路径 "% systemroot% \\ system32 \\DLL1.dll" 和资源标识符 "-12"。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。 有关如何在这些版本的 Windows 上访问设备安装程序类的图标信息的信息，请参阅[访问设备安装程序类的图标属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-icon-properties-of-a-device-setup-class)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiLoadClassIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)

 

 






