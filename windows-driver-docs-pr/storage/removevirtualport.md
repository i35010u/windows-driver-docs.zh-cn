---
title: RemoveVirtualPort 方法
description: RemoveVirtualPort 方法删除特定的全球通用端口名称 (WWPN) 的虚拟端口。
ms.assetid: 47A85B72-821C-4552-BA6E-1742D58B54A4
keywords:
- RemoveVirtualPort 方法存储设备
topic_type:
- apiref
api_name:
- RemoveVirtualPort
api_type:
- COM
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ad9797ed32f6342c250075053b59930097a07844
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368914"
---
# <a name="removevirtualport-method"></a>RemoveVirtualPort 方法


**RemoveVirtualPort**方法中删除特定的全球通用端口名称 (WWPN) 的虚拟端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveVirtualPort(
   [in] uint8   WWPN[8],
   [out] uint16 Status
);
```

<a name="parameters"></a>Parameters
----------

*WWPN\[8\]*    
要删除的虚拟端口的全球通用端口名称。

*状态*   
在返回时包含操作的状态。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[NPIV 状态代码](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn386176(v=vs.85))

 

 






