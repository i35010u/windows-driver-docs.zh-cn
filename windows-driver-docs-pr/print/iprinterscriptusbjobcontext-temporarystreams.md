---
title: IPrinterScriptUsbJobContext TemporaryStreams 方法
description: 返回可由 IHV JavaScript 函数为当前作业使用的永久性数据流的 IPrinterScriptableSequentialStream 接口的数组。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ED9AFB90-287B-4030-AC20-ECCA9841D27E
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
ms.openlocfilehash: c596e7c379d77b866b69c234b32da8a442999654
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844328"
---
# <a name="iprinterscriptusbjobcontexttemporarystreams-method"></a>IPrinterScriptUsbJobContext：： TemporaryStreams 方法

返回可由 IHV JavaScript 函数为当前作业使用的永久性数据流的[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)接口的数组。

<a name="syntax"></a>语法
------

```cpp
HRESULT TemporaryStreams(
  [out, retval] IDispatch **ppArray
);
```

<a name="parameters"></a>参数
----------

*ppArray* \[out，retval\]  
指向[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)接口的数组的指针。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**TemporaryStreams**为只读方法。 对于 IHV JavaScript 函数，最多可以有2个临时流。 这些流仅适用于当前打印作业的持续时间。 IHV 可以使用它来存储尚未准备好发送到打印设备的数据。 在以后的**writePrintData** JavaScript 函数调用中，可以使用这些流将存储的数据发送到打印设备。

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
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p>目标平台</p></td>
<td>桌面</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)
