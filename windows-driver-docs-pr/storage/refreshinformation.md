---
title: RefreshInformation 函数
description: RefreshInformation WMI 方法更新与调用实例对象对应的 HBA 的所有表。
keywords:
- RefreshInformation 函数存储设备
topic_type:
- apiref
api_name:
- RefreshInformation
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6d894b409c93eafe5f7fa430349c4b1d74d9e54f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815847"
---
# <a name="refreshinformation-function"></a>RefreshInformation 函数


**RefreshInformation** WMI 方法更新与调用实例对象对应的 HBA 的所有表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RefreshInformation(void);
```

<a name="parameters"></a>参数
----------

此函数没有参数。

<a name="return-value"></a>返回值
------------

不适用。

<a name="remarks"></a>备注
-------

**RefreshInformation** wmi 方法刷新由以下 WMI 方法检索的端口属性数据：

[**GetDiscoveredPortAttributes**](getdiscoveredportattributes.md)

[**GetFC3MgmtInfo**](getfc3mgmtinfo.md)

[**GetFC4Statistics**](getfc4statistics.md)

[**GetFCPStatistics**](getfcpstatistics.md)

[**GetPortAttributesByWWN**](getportattributesbywwn.md)

此 WMI 方法属于 [MSFC \_ HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetDiscoveredPortAttributes**](getdiscoveredportattributes.md)

[**GetFC3MgmtInfo**](getfc3mgmtinfo.md)

[**GetFC4Statistics**](getfc4statistics.md)

[**GetFCPStatistics**](getfcpstatistics.md)

[**GetPortAttributesByWWN**](getportattributesbywwn.md)

 

 






