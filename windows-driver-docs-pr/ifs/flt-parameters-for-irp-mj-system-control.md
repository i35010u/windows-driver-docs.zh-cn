---
title: FLT_PARAMETERS IRP_MJ_SYSTEM_CONTROL 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_系统\_控件。
ms.assetid: 6f1c34b2-1c79-4372-8b94-afe4b50294d5
keywords:
- FLT_PARAMETERS IRP_MJ_SYSTEM_CONTROL 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 6a00b21b822ad710cf165e6c08fbf3adbc6e2fdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327895"
---
# <a name="fltparameters-for-irpmjsystemcontrol-union"></a>FLT\_IRP 的参数\_MJ\_系统\_控件联合


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作是 IRP\_MJ\_系统\_控件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG_PTR ProviderId;
    PVOID     DataPath;
    ULONG     BufferSize;
    PVOID     Buffer;
  } WMI;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**WMI**  
结构，它包含以下成员。

**ProviderId**  
此参数的含义取决于操作的次要函数代码。 （请参阅以下备注部分。）

**DataPath**  
此参数的含义取决于操作的次要函数代码。 （请参阅以下备注部分。）

**BufferSize**  
此参数的含义取决于操作的次要函数代码。 （请参阅以下备注部分。）

**Buffer**  
此参数的含义取决于操作的次要函数代码。 （请参阅以下备注部分。）

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_系统\_控制操作包含的系统管理操作的参数表示回调数据 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP 的含义\_MJ\_系统\_控制参数取决于次要函数代码。 (请参阅**MinorFunction**的成员[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。)有关详细信息，请参阅以下次要函数代码的引用项：

[**IRP\_MN\_更改\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff550831)

[**IRP\_MN\_更改\_单个\_项**](https://msdn.microsoft.com/library/windows/hardware/ff550836)

[**IRP\_MN\_禁用\_集合**](https://msdn.microsoft.com/library/windows/hardware/ff550848)

[**IRP\_MN\_DISABLE\_EVENTS**](https://msdn.microsoft.com/library/windows/hardware/ff550851)

[**IRP\_MN\_ENABLE\_COLLECTION**](https://msdn.microsoft.com/library/windows/hardware/ff550857)

[**IRP\_MN\_ENABLE\_EVENTS**](https://msdn.microsoft.com/library/windows/hardware/ff550859)

[**IRP\_MN\_EXECUTE\_METHOD**](https://msdn.microsoft.com/library/windows/hardware/ff550868)

[**IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)

[**IRP\_MN\_查询\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)

[**IRP\_MN\_REGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551731)

[**IRP\_MN\_REGINFO\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff551734)

IRP\_MJ\_系统\_控件是一个基于 IRP 的操作。

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

[**IRP\_MN\_更改\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff550831)

[**IRP\_MN\_更改\_单个\_项**](https://msdn.microsoft.com/library/windows/hardware/ff550836)

[**IRP\_MN\_禁用\_集合**](https://msdn.microsoft.com/library/windows/hardware/ff550848)

[**IRP\_MN\_DISABLE\_EVENTS**](https://msdn.microsoft.com/library/windows/hardware/ff550851)

[**IRP\_MN\_ENABLE\_COLLECTION**](https://msdn.microsoft.com/library/windows/hardware/ff550857)

[**IRP\_MN\_ENABLE\_EVENTS**](https://msdn.microsoft.com/library/windows/hardware/ff550859)

[**IRP\_MN\_EXECUTE\_METHOD**](https://msdn.microsoft.com/library/windows/hardware/ff550868)

[**IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)

[**IRP\_MN\_查询\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)

[**IRP\_MN\_REGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551731)

[**IRP\_MN\_REGINFO\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff551734)

 

 






