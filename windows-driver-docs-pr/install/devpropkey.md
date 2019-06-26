---
title: DEVPROPKEY 结构
description: 在 Windows Vista 和更高版本的 Windows，DEVPROPKEY 结构表示统一的设备属性模型中的设备属性的设备属性键。
ms.assetid: 98986d43-84c0-44e6-83f9-08e872ea5e6d
keywords:
- DEVPROPKEY 结构设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROPKEY
api_location:
- devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 00435311f4ee55af17d7a5d7c6f342d9c72796b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372733"
---
# <a name="devpropkey-structure"></a>DEVPROPKEY 结构


在 Windows Vista 和更高版本的 Windows，DEVPROPKEY 结构表示中的设备属性的设备属性键[统一的设备属性模型](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
struct DEVPROPKEY {
  DEVPROPGUID fmtid;
  DEVPROPID   pid;
};
```

<a name="members"></a>成员
-------

**fmtid**  
DEVPROPGUID 类型的一个值，指定的属性类别。

DEVPROPGUID 数据类型的定义如下：

```cpp
typedef GUID  DEVPROPGUID, *PDEVPROPGUID;
```

**pid**  
一个 DEVPROPID 类型化值，该值唯一标识内的属性类别的属性。 内部系统方面的考虑，属性标识符必须大于或等于 2。

DEVPROPID 数据类型的定义如下：

```cpp
typedef ULONG DEVPROPID, *PDEVPROPID;
```

<a name="remarks"></a>备注
-------

DEVPROPKEY 结构属于[统一的设备属性模型](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)。

中定义一组基本的系统提供的设备属性键*Devpkey.h*。

[**定义\_DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/define-devpropkey)宏创建 DEVPROPKEY 结构，它表示设备属性键的实例。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEFINE\_DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/define-devpropkey)

 

 






