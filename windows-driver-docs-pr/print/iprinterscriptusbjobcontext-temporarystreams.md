---
title: IPrinterScriptUsbJobContext TemporaryStreams 方法
description: 返回可由 IHV JavaScript 函数为当前作业使用的永久性数据流的 IPrinterScriptableSequentialStream 接口的数组。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- TemporaryStreams 方法打印设备
- TemporaryStreams 方法打印设备，IPrinterScriptUsbJobContext 接口
- IPrinterScriptUsbJobContext 接口打印设备，TemporaryStreams 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.TemporaryStreams
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384812f12814258c6edb3f26a2ea033e3509ec16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796595"
---
# <a name="iprinterscriptusbjobcontexttemporarystreams-method"></a>IPrinterScriptUsbJobContext：： TemporaryStreams 方法

返回可由 IHV JavaScript 函数为当前作业使用的永久性数据流的 [IPrinterScriptableSequentialStream](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream) 接口的数组。

<a name="syntax"></a>语法
------

```cpp
HRESULT TemporaryStreams(
  [out, retval] IDispatch **ppArray
);
```

<a name="parameters"></a>参数
----------

*ppArray* \[out，retval\]  
指向 [IPrinterScriptableSequentialStream](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream) 接口的数组的指针。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**TemporaryStreams** 为只读方法。 对于 IHV JavaScript 函数，最多可以有2个临时流。 这些流仅适用于当前打印作业的持续时间。 IHV 可以使用它来存储尚未准备好发送到打印设备的数据。 在以后的 **writePrintData** JavaScript 函数调用中，可以使用这些流将存储的数据发送到打印设备。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p>目标平台</p></td>
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[IPrinterScriptableSequentialStream](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)
