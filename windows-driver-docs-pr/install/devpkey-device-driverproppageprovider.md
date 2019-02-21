---
title: DEVPKEY_Device_DriverPropPageProvider
description: DEVPKEY_Device_DriverPropPageProvider
ms.assetid: 9dabdba0-e179-467b-b0ad-960033a7ab86
keywords:
- DEVPKEY_Device_DriverPropPageProvider 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverPropPageProvider
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 51a2d8d6c8b91ec7b60d047dd43d4ba8b8879cb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540589"
---
# <a name="devpkeydevicedriverproppageprovider"></a>DEVPKEY_Device_DriverPropPageProvider


DEVPKEY_Device_DriverPropPageProvider 设备属性表示一个 DLL 和中注册为设备实例的属性页提供程序的 DLL 的入口点的名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverPropPageProvider</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_ENUMPROPPAGES_32</p>
<p><strong>EnumPropPages32</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用设置的值 DEVPKEY_Device_DriverPropPageProvider [ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)附带[ **INF *DDInstall*一节**](https://msdn.microsoft.com/library/windows/hardware/ff547344)安装设备的 INF 文件。

可以通过调用检索的值 DEVPKEY_Device_DriverPropPageProvider [ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_DriverPropPageProvider 属性键。 在这些早期版本的 Windows 中，您可以访问此属性的值，通过访问对应**EnumPropPages32**设备实例软件项下的注册表值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备驱动程序属性](https://msdn.microsoft.com/library/windows/hardware/ff537732)。

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

[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






