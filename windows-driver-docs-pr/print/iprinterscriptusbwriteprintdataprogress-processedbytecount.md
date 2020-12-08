---
title: 'IPrinterScriptUsbWritePrintDataProgress ProcessedByteCount 方法 (out) '
description: 返回在调用此方法时由 IHV JavaScript 函数处理的字节数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- ProcessedByteCount 方法打印设备
- ProcessedByteCount 方法打印设备，IPrinterScriptUsbWritePrintDataProgress 接口
- IPrinterScriptUsbWritePrintDataProgress 接口打印设备，ProcessedByteCount 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress.ProcessedByteCount
api_type:
- COM
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 91bc6427a8cf335dfa2ac8a544a1297054eb1c8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835539"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method-out"></a>IPrinterScriptUsbWritePrintDataProgress：:P rocessedByteCount 方法 (out) 

返回在调用此方法时由 IHV JavaScript 函数处理的字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT ProcessedByteCount(
  [out, retval] UINT32 *value
);
```

## <a name="parameters"></a>参数

*值* \[out，retval\]  
调用此方法时处理的字节数。

## <a name="return-value"></a>返回值

此方法返回 **HRESULT** 值。

## <a name="requirements"></a>要求

**支持的最低客户端：** Windows 8.1

**支持的最低服务器：** Windows Server 2012 R2

**目标平台：** 机

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
