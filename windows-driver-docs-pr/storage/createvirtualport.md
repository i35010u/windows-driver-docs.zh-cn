---
title: CreateVirtualPort 方法
description: CreateVirtualPort 方法创建的虚拟端口特定的全球通用端口名称 (WWPN)。
ms.assetid: B4274FB7-2850-4E17-ACDE-5592B0390E8B
keywords:
- CreateVirtualPort 方法存储设备
topic_type:
- apiref
api_name:
- CreateVirtualPort
api_type:
- COM
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8bab66a53593ea632f35c83dc5c59e881098045e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545498"
---
# <a name="createvirtualport-method"></a>CreateVirtualPort 方法


**CreateVirtualPort**方法创建的虚拟端口特定的全球通用端口名称 (WWPN)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void CreateVirtualPort(
   [in] uint8   WWPN[8],
   [in] uint8   WWNN[8],
   [in] uint8   Tag[16],
   [in] uint16  VirtualName[64],
   [out] uint16 Status
);
```

<a name="parameters"></a>参数
----------

*WWPN\[8\]*   
要创建的虚拟端口的全球通用端口名称。

*WWNN\[8\]*   
要将与虚拟端口关联的全球通用节点名称。

*Tag\[16\]*   
虚拟端口标记标识符。

*VirtualName\[64\]*   
虚拟端口的符号名称。

*状态*   
在返回时包含操作的状态。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[NPIV 状态代码](https://msdn.microsoft.com/library/windows/hardware/dn386176)

 

 






