---
title: WDF_PTR_ADD_OFFSET 宏
description: WDF_PTR_ADD_OFFSET 宏将偏移值添加到地址，并返回生成的地址。
ms.assetid: 21402be4-ef71-4828-b588-d178d66472e5
keywords:
- WDF_PTR_ADD_OFFSET 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2a8e0ebf83afde8456a51312cd71dca8b83e2df
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187749"
---
# <a name="wdf_ptr_add_offset-macro"></a>WDF_PTR_ADD_OFFSET 宏


**WDF_PTR_ADD_OFFSET**宏将偏移值添加到地址，并返回生成的地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID WDF_PTR_ADD_OFFSET(
    _ptr,
    _offset
);
```

<a name="parameters"></a>参数
----------

*_ptr*   
指定地址。

*_offset*   
指定偏移量值（以字节为单位）。

<a name="return-value"></a>返回值
------------

返回一个指向生成的地址的指针。

<a name="remarks"></a>备注
-------

此宏调用 [**WDF_PTR_ADD_OFFSET_TYPE**](wdf-ptr-add-offset-type.md) ，并将 *_type* 参数设置为 PVOID。

宏的定义如下：

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET(_ptr, _offset) \
        WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, PVOID)
```

下面是 Toaster 示例 (Toaster \\ 函数函数示例) 的 \\ 示例 \\ 。 在此示例中，驱动程序调用 **WDF_PTR_ADD_OFFSET** 以添加地址的偏移量，以确定要传递到 [**WDF_WMI_BUFFER_APPEND_STRING**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdf_wmi_buffer_append_string) 函数的目标缓冲区地址。

```cpp
        //
        // Write the instance name
        //
        size -= wnodeSize;
        status = WDF_WMI_BUFFER_APPEND_STRING(
            WDF_PTR_ADD_OFFSET(wnode, wnode->OffsetInstanceName),
            size,
            &deviceName,
            &length
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
            &modelName,
            &length
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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfcore (包含 Wdf .h) </td>
</tr>
</tbody>
</table>