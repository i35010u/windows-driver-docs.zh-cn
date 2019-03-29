---
title: WDF_PTR_ADD_OFFSET 宏
description: WDF_PTR_ADD_OFFSET 宏将偏移量的值添加到地址，并返回生成的地址。
ms.assetid: 21402be4-ef71-4828-b588-d178d66472e5
keywords:
- WDF_PTR_ADD_OFFSET 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1af84b12017ede07c9785dd21c357ddc84087faf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566313"
---
# <a name="wdfptraddoffset-macro"></a>WDF_PTR_ADD_OFFSET 宏


**WDF_PTR_ADD_OFFSET**宏将偏移量的值添加到地址，并返回生成的地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID WDF_PTR_ADD_OFFSET(
    _ptr,
    _offset
);
```

<a name="parameters"></a>Parameters
----------

*_ptr*   
指定的地址。

*_offset*   
以字节为单位指定偏移量的值。

<a name="return-value"></a>返回值
------------

返回一个指向生成的地址。

<a name="remarks"></a>备注
-------

此宏将调用[ **WDF_PTR_ADD_OFFSET_TYPE** ](wdf-ptr-add-offset-type.md)与*类型 （_t)* 参数设置为 PVOID。

定义宏，如下所示：

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET(_ptr, _offset) \
        WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, PVOID)
```

下面是一个示例中的 Toaster 示例 (toaster\\func\\特色\\wmi.c)。 在示例中，该驱动程序调用**WDF_PTR_ADD_OFFSET**若要将某一偏移量添加到的地址来确定要传递到目标缓冲区地址[ **WDF_WMI_BUFFER_APPEND_STRING** ](https://msdn.microsoft.com/library/windows/hardware/ff553057)函数。

```cpp
        //
        // Write the instance name
        //
        size -= wnodeSize;
        status = WDF_WMI_BUFFER_APPEND_STRING(
            WDF_PTR_ADD_OFFSET(wnode, wnode->OffsetInstanceName),
            size,
            &amp;deviceName,
            &amp;length
            );

        //
        // Size was precomputed, this should never fail
        //
        ASSERT(NT_SUCCESS(status));


        //
        // Write the data, which is the model name as a string
        //
        size -= wnodeInstanceNameSize;
        WDF_WMI_BUFFER_APPEND_STRING(
            WDF_PTR_ADD_OFFSET(wnode,  wnode->DataBlockOffset),
            size,
            &amp;modelName,
            &amp;length
            );
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfcore.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>










