---
title: CreateVirtualPort 方法
description: CreateVirtualPort 方法将创建具有特定全球通用端口名称 (WWPN) 的虚拟端口。
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
ms.openlocfilehash: 7fbe1ca89c01d0d8fbca063108154a58d7dc1b9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811745"
---
# <a name="createvirtualport-method"></a>CreateVirtualPort 方法


**CreateVirtualPort** 方法将创建具有特定全球通用端口名称 (WWPN) 的虚拟端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void CreateVirtualPort(
   [in] uint8   WWPN[8],
   [in] uint8   WWNN[8],
   [in] uint8   Tag[16],
   [in] uint16  VirtualName[64],
   [out] uint16 Status
);
```

<a name="parameters"></a>参数
----------

*WWPN \[ 8\]*   
要创建的虚拟端口的全球通用端口名称。

*WWNN \[ 8\]*   
要与虚拟端口关联的全球通用节点名称。

*标记 \[ 16\]*   
虚拟端口的标记标识符。

*VirtualName \[ 64\]*   
虚拟端口的符号名称。

*状态*   
返回时，包含操作的状态。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[NPIV 状态代码](/previous-versions/windows/hardware/drivers/dn386176(v=vs.85))

 

