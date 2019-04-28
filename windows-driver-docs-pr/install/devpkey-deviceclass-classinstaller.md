---
title: DEVPKEY_DeviceClass_ClassInstaller
description: DEVPKEY_DeviceClass_ClassInstaller
ms.assetid: 7bde624e-37e5-4603-bf8c-1122b7090ab2
keywords:
- DEVPKEY_DeviceClass_ClassInstaller 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassInstaller
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e3b8521ecccdda90791ae2660a3f45c3f1ae1947
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339647"
---
# <a name="devpkeydeviceclassclassinstaller"></a>DEVPKEY_DeviceClass_ClassInstaller


DEVPKEY_DeviceClass_ClassInstaller 设备属性表示的类安装程序[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_ClassInstaller</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>"<em>class-installer</em>.dll,<em>class-entry-point</em>"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>Installer32</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_DeviceClass_ClassInstaller 的值为的值**Installer32**类注册表项下的注册表值。 此条目包含类安装程序 DLL 的名称和设备安装程序类安装程序的入口点。

**Installer32**可以设置注册表值以查找设备安装程序类[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INFClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)的安装设备安装程序类的 INF 文件。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值ClassInstaller。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_ClassInstaller 属性键。 可以通过访问对应访问此属性的值**Installer32**类注册表项下的注册表值。 有关如何对访问类注册表项下的值项的信息，请参阅[访问注册表项值下类注册表项](https://msdn.microsoft.com/library/windows/hardware/ff537751)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






