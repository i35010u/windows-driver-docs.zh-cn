---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.assetid: d1f1d6f2-154e-4e41-8ebf-4071de4ceafe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0f34130b17bfcd6a4f3434c538050b23717eca60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377213"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret**方法建立发起程序，它将验证目标的发起方的质询响应时要使用的共享的机密。

发起方使用两个不同的共享的机密来实现质询握手身份验证协议 (CHAP):

-   **SetCHAPSharedSecret**方法可创建发起方使用来验证目标的发起方的质询响应的共享的机密。

-   [LoginToTarget](logintotarget.md)方法可创建发起方将使用生成的 CHAP 目标的质询响应的共享的机密。

**SetCHAPSharedSecret** WMI 方法属于未发布[MSiSCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关参数的说明**SetCHAPSharedSecret**方法，请参阅成员的说明[ **SetCHAPSharedSecret\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565595)和[**SetCHAPSharedSecret\_出**](https://msdn.microsoft.com/library/windows/hardware/ff565600)结构。

微型端口驱动程序实现 MSiSCSI\_操作 WMI 类不支持所需**SetCHAPSharedSecret**。

 

 





