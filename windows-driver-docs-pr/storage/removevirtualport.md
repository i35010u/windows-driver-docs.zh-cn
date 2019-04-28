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
ms.openlocfilehash: 9276b12ec7d0b8e9c5238bc526f2d66b518e02a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349143"
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


[NPIV 状态代码](https://msdn.microsoft.com/library/windows/hardware/dn386176)

 

 






