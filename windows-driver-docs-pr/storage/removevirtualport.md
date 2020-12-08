---
title: RemoveVirtualPort 方法
description: RemoveVirtualPort 方法)  (WWPN 中删除特定全球通用端口名称的虚拟端口。
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
ms.openlocfilehash: 7e96ebb0ab5d9eeade472f08ff04c9c3943c08e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813483"
---
# <a name="removevirtualport-method"></a>RemoveVirtualPort 方法


**RemoveVirtualPort** 方法)  (WWPN 中删除特定全球通用端口名称的虚拟端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveVirtualPort(
   [in] uint8   WWPN[8],
   [out] uint16 Status
);
```

<a name="parameters"></a>参数
----------

*WWPN \[ 8\]*   
要删除的虚拟端口的全球通用端口名称。

*状态*   
返回时，包含操作的状态。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[NPIV 状态代码](/previous-versions/windows/hardware/drivers/dn386176(v=vs.85))

 

