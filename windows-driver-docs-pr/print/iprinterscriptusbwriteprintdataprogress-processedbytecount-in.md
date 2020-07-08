---
title: IPrinterScriptUsbWritePrintDataProgress ProcessedByteCount 方法（在中）
description: 设置在调用此方法时 IHV JavaScript 函数已处理的字节数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 9E870B80-421B-496A-9510-D97D3A4D7892
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
ms.openlocfilehash: be5165e4be597e67da9cf20183368b4c6dae6090
ms.sourcegitcommit: c2c99017178160988aa0e9a861ac347a11cda12a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86092464"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method-in"></a>IPrinterScriptUsbWritePrintDataProgress：:P rocessedByteCount 方法（在中）

设置在调用此方法时 IHV JavaScript 函数已处理的字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT ProcessedByteCount(
  [in]  UINT32 value
);
```

## <a name="parameters"></a>参数

*值* \[中\]  
调用此方法时处理的字节数。

## <a name="return-values"></a>返回值

此方法返回**HRESULT**值。

## <a name="requirements"></a>要求

**支持的最低客户端：** Windows 8.1

**支持的最低服务器：** Windows Server 2012 R2

**目标平台：** 机

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
