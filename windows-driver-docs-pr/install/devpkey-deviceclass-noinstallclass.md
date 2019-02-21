---
title: DEVPKEY_DeviceClass_NoInstallClass
description: DEVPKEY_DeviceClass_NoInstallClass
ms.assetid: 4b4f1187-570b-40e0-a96c-f3511f46a1be
keywords:
- DEVPKEY_DeviceClass_NoInstallClass 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_NoInstallClass
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c7346e6c70adc19aa020aef0753998df05a144f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548292"
---
# <a name="devpkeydeviceclassnoinstallclass"></a>DEVPKEY_DeviceClass_NoInstallClass


DEVPKEY_DeviceClass_NoInstallClass 设备安装程序类属性表示一个布尔值标志，用于控制是否在设备[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)中显示**添加硬件向导**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_NoInstallClass</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>NoInstallClass</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_DeviceClass_NoInstallClass 将值设置为 DEVPROP_TRUE 指示的类中的设备安装不需要最终用户交互。 如果此值未设置为 DEVPROP_TRUE，添加硬件向导会显示设备安装程序类的设备。

**NoInstallClass**可以设置注册表值以查找设备安装程序类[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INFClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)的安装类的 INF 文件。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值NoInstallClass。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_NoInstallClass 属性键。 可以通过访问对应访问此属性的值**NoInstallClass**类注册表项下的注册表值。 有关如何对访问类注册表项下的值项的信息，请参阅[访问注册表项值下类注册表项](https://msdn.microsoft.com/library/windows/hardware/ff537751)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






