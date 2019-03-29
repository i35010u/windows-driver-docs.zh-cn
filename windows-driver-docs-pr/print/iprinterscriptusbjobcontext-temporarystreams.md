---
title: IPrinterScriptUsbJobContext TemporaryStreams 方法
description: 返回可用于当前作业由 IHV JavaScript 函数的持久性数据流的 IPrinterScriptableSequentialStream 接口的数组。
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
ms.openlocfilehash: b1f44c1332415f4cd5ac98d450b87dcec3cdea37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563418"
---
# <a name="iprinterscriptusbjobcontexttemporarystreams-method"></a>IPrinterScriptUsbJobContext::TemporaryStreams 方法

返回的数组[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)持久性数据流可用于当前作业由 IHV JavaScript 函数的接口。

<a name="syntax"></a>语法
------

```cpp
HRESULT TemporaryStreams(
  [out, retval] IDispatch **ppArray
);
```

<a name="parameters"></a>Parameters
----------

*ppArray* \[out，retval\]  
指向数组的指针[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)接口。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**TemporaryStreams**是只读的方法。 有 2 个临时流最多可供 IHV JavaScript 函数。 这些流当前打印作业的持续时间内才可用。 IHV 可以使用此存储还未准备好要发送到打印设备的数据。 在更高版本**writePrintData** JavaScript 函数调用，这些流可用于将存储的数据发送到打印设备。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)
