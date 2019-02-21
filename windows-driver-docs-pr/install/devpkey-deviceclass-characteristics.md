---
title: DEVPKEY_DeviceClass_Characteristics
description: DEVPKEY_DeviceClass_Characteristics
ms.assetid: dd50a97b-7230-46a5-b6d2-0f741d7ae5d4
keywords:
- DEVPKEY_DeviceClass_Characteristics 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Characteristics
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 529164eb6008871299e140dbe4bbcd98c3a1159c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533792"
---
# <a name="devpkeydeviceclasscharacteristics"></a>DEVPKEY_DeviceClass_Characteristics


DEVPKEY_DeviceClass_Characteristics 设备属性表示中的所有设备的默认设备特征[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Characteristics</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和设备安装程序类安装后的安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_CHARACTERISTICS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

安装应用程序安装设备安装程序类时，可以设置 DEVPKEY_DeviceClass_Characteristics 的值。 有关如何安装设备安装程序类和设置此属性的信息，请参阅[ **INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)以及注册表条目值的相关信息**DeviceCharacteristics**中提供的"特殊*值项名称*关键字"部分中的[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

DEVPKEY_DeviceClass_Characteristics 的值是 FILE_DEVICE_ 的按位 OR*Xxx*中定义的标志*wdm.h 中*并*Ntddk.h*。 有关设备特征的详细信息，请参阅*DeviceCharacteristics*的参数[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)函数。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索 DEVPKEY_DeviceClass_ 值特征。

Windows Server 2003 和 Windows XP 支持此属性，但不是支持 DEVPKEY_DeviceClass_Characteristics 属性键。 在这些早期版本的 Windows 中，可以使用 SPCRP_CHARACTERISTICS 标识符来访问此属性的值。 有关如何访问此属性的值的信息，请参阅[检索设备安装程序类 SPCRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff550644)。

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


[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)

[**INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






