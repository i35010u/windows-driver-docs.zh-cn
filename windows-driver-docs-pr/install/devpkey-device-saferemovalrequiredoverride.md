---
title: DEVPKEY_Device_SafeRemovalRequiredOverride
description: DEVPKEY_Device_SafeRemovalRequiredOverride
ms.assetid: 8289effe-3849-41bf-b870-69e3d8cb8850
keywords:
- DEVPKEY_Device_SafeRemovalRequiredOverride 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SafeRemovalRequiredOverride
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a802b18e53834bd36ae655177f994ee920c05767
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546626"
---
# <a name="devpkeydevicesaferemovalrequiredoverride"></a>DEVPKEY_Device_SafeRemovalRequiredOverride


DEVPKEY_Device_SafeRemovalRequiredOverride 设备属性表示设备实例的安全删除重写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_SafeRemovalRequiredOverride</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用此设备属性重写该 Windows 即插即用的启发式结果和 Play (PnP) 用于计算的值[ **DEVPKEY_Device_SafeRemovalRequired** ](devpkey-device-saferemovalrequired.md)设备属性。 此替代执行，如下所示：

-   如果 DEVPKEY_Device_SafeRemovalRequiredOverride 设备属性设置为 DEVPROP_TRUE 并且设备实例是可移除或具有可移动的前身，即插即用集 DEVPROP_TRUE DEVPKEY_Device_SafeRemovalRequired 设备属性，不使用启发式方法。

    **请注意**  设备实例被视为可移动如果其可移动设备功能设置。 有关详细信息，请参阅[可移动设备功能的概述](https://msdn.microsoft.com/library/windows/hardware/ff549564)。

     

-   如果 DEVPKEY_Device_SafeRemovalRequiredOverride 设备属性设置为 DEVPROP_TRUE 和设备实例 （或祖先） 不是可移动的、 即插即用可设置到 DEVPROP_FALSE DEVPKEY_Device_SafeRemovalRequired 并不使用启发式方法。

-   如果 DEVPKEY_Device_SafeRemovalRequiredOverride 设备属性未设置，或者设置为 DEVPROP_FALSE，即插即用 DEVPKEY_Device_SafeRemovalRequired 设备属性设置为一个值，通过使用启发式方法确定该值。

可以通过调用检索的值 DEVPKEY_Device_SafeRemovalRequiredOverride [ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)。 此外可以设置此值，通过调用[ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)。

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163)

 

 






