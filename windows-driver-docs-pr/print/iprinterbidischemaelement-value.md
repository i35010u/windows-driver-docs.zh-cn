---
title: IPrinterBidiSchemaElement Value 方法
description: Value 方法返回 Bidi 架构元素的值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: F989AFEF-795D-4C1A-880D-58CBC2D2B021
keywords:
- 值方法打印设备
- 值方法打印设备，IPrinterBidiSchemaElement 接口
- IPrinterBidiSchemaElement 接口打印设备，Value 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.Value
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 093e89237a40fe25e9428848e8f0db8995161e56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564806"
---
# <a name="iprinterbidischemaelementvalue-method"></a>IPrinterBidiSchemaElement::Value 方法

Value 方法返回 Bidi 架构元素的值。

<a name="syntax"></a>语法
------

```cpp
HRESULT Value(
  [out, retval] VARIANT *pValue
);
```

<a name="parameters"></a>Parameters
----------

*pValue* \[out, retval\]  
返回的元素值中。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)
