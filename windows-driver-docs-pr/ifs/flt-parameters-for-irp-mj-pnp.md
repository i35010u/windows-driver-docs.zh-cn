---
title: FLT_PARAMETERS IRP_MJ_PNP 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_PNP。
ms.assetid: d3ce893b-f113-4c50-8f52-30c7ced25ae0
keywords:
- FLT_PARAMETERS IRP_MJ_PNP 联合可安装文件系统驱动程序
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f41c12635a72139b79a0376bb01282a102ec709d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360349"
---
# <a name="fltparameters-for-irpmjpnp-union"></a>FLT\_IRP 的参数\_MJ\_即插即用的并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct  StartDevice;
    struct  QueryDeviceRelations;
    struct  QueryInterface;
    struct  DeviceCapabilities;
    struct  FilterResourceRequirements;
    struct  ReadWriteConfig;
    struct  SetLock;
    struct  QueryId;
    struct  QueryDeviceText;
    struct  UsageNotification;
  } Pnp;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**Pnp**  
**StartDevice**  
联合组件用于 IRP\_MN\_启动\_设备操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)。

**QueryDeviceRelations**  
联合组件用于 IRP\_MN\_查询\_设备\_关系操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)。

**QueryInterface**  
联合组件用于 IRP\_MN\_查询\_接口操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)。

**DeviceCapabilities**  
联合组件用于 IRP\_MN\_查询\_功能操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)。

**FilterResourceRequirements**  
联合组件用于 IRP\_MN\_筛选器\_资源\_要求操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_筛选器\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff550874).

**ReadWriteConfig**  
联合组件用于 IRP\_MN\_读取\_配置和 IRP\_MN\_编写\_配置操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_读取\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)和[ **IRP\_MN\_编写\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551769)。

**SetLock**  
联合组件用于 IRP\_MN\_设置\_锁定操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_设置\_锁**](https://msdn.microsoft.com/library/windows/hardware/ff551742)。

**QueryId**  
联合组件用于 IRP\_MN\_查询\_ID 操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_查询\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)。

**QueryDeviceText**  
联合组件用于 IRP\_MN\_查询\_设备\_文本操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_查询\_设备\_文本**](https://msdn.microsoft.com/library/windows/hardware/ff551674)。

**UsageNotification**  
联合组件用于 IRP\_MN\_设备\_用法\_通知操作。 有关此操作的参数的详细信息，请参阅引用条目[ **IRP\_MN\_设备\_使用情况\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841).

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_PNP** ](irp-mj-pnp.md)操作包含表示的回调数据基于 IRP 的插 (PnP) 操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。

IRP\_MJ\_即插即用的操作是基于 IRP 的操作。

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
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_PNP （WDK 内核模式驱动程序体系结构参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

[**IRP\_MN\_DEVICE\_USAGE\_NOTIFICATION**](https://msdn.microsoft.com/library/windows/hardware/ff550841)

[**IRP\_MN\_FILTER\_RESOURCE\_REQUIREMENTS**](https://msdn.microsoft.com/library/windows/hardware/ff550874)

[**IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

[**IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)

[**IRP\_MN\_QUERY\_DEVICE\_TEXT**](https://msdn.microsoft.com/library/windows/hardware/ff551674)

[**IRP\_MN\_查询\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)

[**IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)

[**IRP\_MN\_READ\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551727)

[**IRP\_MN\_SET\_LOCK**](https://msdn.microsoft.com/library/windows/hardware/ff551742)

[**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)

[**IRP\_MN\_WRITE\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551769)

 

 






