---
title: DEVPKEY_Device_MatchingDeviceId
description: DEVPKEY_Device_MatchingDeviceId
ms.assetid: 4695c713-0586-42be-9dd7-7da5bd87a3c0
keywords:
- DEVPKEY_Device_MatchingDeviceId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_MatchingDeviceId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8348b275652f6bc03f35c85acdcaaa686db52b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351081"
---
# <a name="devpkeydevicematchingdeviceid"></a>DEVPKEY_Device_MatchingDeviceId


DEVPKEY_Device_MatchingDeviceId 设备属性表示[硬件 ID](https://msdn.microsoft.com/library/windows/hardware/ff546152)或[兼容 ID](https://msdn.microsoft.com/library/windows/hardware/ff539950) Windows 使用来安装设备实例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_MatchingDeviceId</p></td>
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
<td align="left"><p>REGSTR_VAL_MATCHINGDEVICEID</p>
<p><strong>MatchingDeviceId</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_MatchingDeviceId 的值。 由提供的硬件 Id 和设备兼容 Id*设备描述*中包含的条目[ **INF*模型*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)安装设备的 INF 文件。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 PKEY_Device_MatchingDeviceId 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_MatchingDeviceId 属性键。 在这些早期版本的 Windows 中，您可以访问此属性的值，通过访问对应**MatchingDeviceId**设备实例软件项下的注册表值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备驱动程序属性](https://msdn.microsoft.com/library/windows/hardware/ff537732)。

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


[**INF*模型*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






