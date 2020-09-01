---
title: RemoveVirtualPort 方法
description: RemoveVirtualPort 方法)  (WWPN 中删除特定全球通用端口名称的虚拟端口。
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
ms.openlocfilehash: 8f3408ec5bd31c6abea3d5961656c23b2e29cf83
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191119"
---
# <a name="removevirtualport-method"></a>RemoveVirtualPort 方法


**RemoveVirtualPort**方法)  (WWPN 中删除特定全球通用端口名称的虚拟端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveVirtualPort(
   [in] uint8   WWPN[8],
   [out] uint16 Status
);
```

<a name="parameters"></a>参数
----------

*WWPN \[ 8\]*   
要删除的虚拟端口的全球通用端口名称。

*状态值*   
返回时，包含操作的状态。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[NPIV 状态代码](/previous-versions/windows/hardware/drivers/dn386176(v=vs.85))

 

