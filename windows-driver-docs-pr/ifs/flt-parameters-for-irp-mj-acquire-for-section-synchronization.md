---
title: FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合
description: 该操作的 FLT_IO_PARAMETER_BLOCK 结构在 MajorFunction 字段 IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 时使用以下联合组件。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合可安装文件系统驱动程序
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
ms.openlocfilehash: af83db238aa83ab081c913ce0f81de390e631495
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522368"
---
# <a name="fltparameters-for-irpmjacquireforsectionsynchronization-union"></a>FLT\_IRP 的参数\_MJ\_ACQUIRE\_有关\_部分\_同步并集


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构，该操作是 IRP\_MJ\_ACQUIRE\_有关\_部分\_同步。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    FS_FILTER_SECTION_SYNC_TYPE SyncType;
    ULONG POINTER_ALIGNMENT     PageProtection;
    PFS_FILTER_SECTION_SYNC_OUTPUT OutputInformation;
  } AcquireForSectionSynchronization;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SyncType**  
* 指定请求的部分的同步的类型。 此参数必须为两个枚举值之一：
  * **SyncTypeCreateSection**
  * **SyncTypeOther**

**PageProtection**  
* 指定为部分中请求的页保护类型。 必须为零**SyncType**是 SyncTypeOther。 否则，以下标记之一，可能需要与页面合并\_NOCACHE:

  * 页\_READONLY

  * 页\_READWRITE

  * 页\_WRITECOPY

  * 页\_EXECUTE

**OutputInformation**
*  一个[ **FS_FILTER_SECTION_SYNC_OUTPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fs_filter_section_sync_output)结构，它指定描述正在创建的节的属性的信息。

## <a name="remarks"></a>备注


[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_采集\_为\_部分\_同步操作包含的参数**AcquireForSectionSynchronization**表示的回调数据操作 ([**FLT\_回调\_数据** ](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_ACQUIRE\_有关\_部分\_同步是文件系统 (FSFilter) 回调操作。

如果的枚举的值**SyncType**成员设置为**SyncTypeOther** （零），文件系统微筛选器或旧版的筛选器驱动程序不能使此操作失败。 如果**SyncType**设置为**SyncTypeCreateSection**，允许文件系统微筛选器或旧版筛选器驱动程序失败，此时状态\_不足\_资源错误如果没有足够的内存来创建部分。

有关 FSFilter 回调操作的详细信息，请参阅引用条目[ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)。

## <a name="requirements"></a>要求


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)

 

 






