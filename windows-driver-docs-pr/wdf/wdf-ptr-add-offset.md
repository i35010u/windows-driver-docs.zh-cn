---
title: WDF_PTR_ADD_OFFSET 宏
description: WDF_PTR_ADD_OFFSET 宏将偏移值添加到地址，并返回生成的地址。
ms.assetid: 21402be4-ef71-4828-b588-d178d66472e5
keywords:
- WDF_PTR_ADD_OFFSET 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d25e5af8889f724cfd0e345276a60869b980ef9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845413"
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

此宏调用[**WDF_PTR_ADD_OFFSET_TYPE**](wdf-ptr-add-offset-type.md) ，并将 *_type*参数设置为 PVOID。

宏的定义如下：

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET(_ptr, _offset) \
        WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, PVOID)
```

下面是 Toaster 示例（Toaster\\func\\\\）的示例。 在此示例中，驱动程序调用**WDF_PTR_ADD_OFFSET**以添加地址的偏移量，以确定要传递到[**WDF_WMI_BUFFER_APPEND_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdf_wmi_buffer_append_string)函数的目标缓冲区地址。

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">全局</a></td>
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
<td><p>标头</p></td>
<td>Wdfcore （包含 Wdf .h）</td>
</tr>
</tbody>
</table>










