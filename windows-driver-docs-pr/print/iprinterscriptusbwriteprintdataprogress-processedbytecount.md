---
title: IPrinterScriptUsbWritePrintDataProgress ProcessedByteCount 方法（out）
description: 返回在调用此方法时由 IHV JavaScript 函数处理的字节数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 667DDBEA-14DA-4037-98A1-A2E7DB8B97F5
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
ms.openlocfilehash: 73ebb2f33889462eb5537c741e235923c4fe792e
ms.sourcegitcommit: c2c99017178160988aa0e9a861ac347a11cda12a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86092466"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method-out"></a>IPrinterScriptUsbWritePrintDataProgress：:P rocessedByteCount 方法（out）

返回在调用此方法时由 IHV JavaScript 函数处理的字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT ProcessedByteCount(
  [out, retval] UINT32 *value
);
```

## <a name="parameters"></a>参数

*值* \[out，retval\]  
调用此方法时处理的字节数。

## <a name="return-value"></a>返回值

此方法返回**HRESULT**值。

## <a name="requirements"></a>要求

**支持的最低客户端：** Windows 8.1

**支持的最低服务器：** Windows Server 2012 R2

**目标平台：** 机

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
