---
title: RefreshInformation 函数
description: RefreshInformation WMI 方法更新 HBA，它对应于调用实例对象的所有表。
ms.assetid: da78db30-0498-4d44-b5bc-76d08dc15938
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
ms.openlocfilehash: bcf4080e89dd4e018cb4db99ed21e9d7fb78818d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366357"
---
# <a name="refreshinformation-function"></a>RefreshInformation 函数


**RefreshInformation** WMI 方法与调用实例对象相对应的 hba 更新所有表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RefreshInformation(void);
```

<a name="parameters"></a>Parameters
----------

此函数没有任何参数。

<a name="return-value"></a>返回值
------------

不适用。

<a name="remarks"></a>备注
-------

**RefreshInformation** WMI 方法刷新由以下 WMI 方法检索到的端口属性数据：

[**GetDiscoveredPortAttributes**](getdiscoveredportattributes.md)

[**GetFC3MgmtInfo**](getfc3mgmtinfo.md)

[**GetFC4Statistics**](getfc4statistics.md)

[**GetFCPStatistics**](getfcpstatistics.md)

[**GetPortAttributesByWWN**](getportattributesbywwn.md)

此 WMI 方法属于[MSFC\_HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetDiscoveredPortAttributes**](getdiscoveredportattributes.md)

[**GetFC3MgmtInfo**](getfc3mgmtinfo.md)

[**GetFC4Statistics**](getfc4statistics.md)

[**GetFCPStatistics**](getfcpstatistics.md)

[**GetPortAttributesByWWN**](getportattributesbywwn.md)

 

 






