---
title: IPrinterBidiSchemaElement 值方法
description: 值方法返回双向架构元素值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 值方法打印设备
- 值方法打印设备，IPrinterBidiSchemaElement 接口
- IPrinterBidiSchemaElement 接口打印设备，值方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.Value
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 326be0edea3fa4094763b03fbfa9b936f8b02a57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796627"
---
# <a name="iprinterbidischemaelementvalue-method"></a>IPrinterBidiSchemaElement：： Value 方法

值方法返回双向架构元素值。

<a name="syntax"></a>语法
------

```cpp
HRESULT Value(
  [out, retval] VARIANT *pValue
);
```

<a name="parameters"></a>参数
----------

*pValue* \[out，retval\]  
返回的元素值。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)
