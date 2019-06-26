---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.assetid: d1f1d6f2-154e-4e41-8ebf-4071de4ceafe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 79549f67a3964126b7be32758f99732876c37742
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374637"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret**方法建立发起程序，它将验证目标的发起方的质询响应时要使用的共享的机密。

发起方使用两个不同的共享的机密来实现质询握手身份验证协议 (CHAP):

-   **SetCHAPSharedSecret**方法可创建发起方使用来验证目标的发起方的质询响应的共享的机密。

-   [LoginToTarget](logintotarget.md)方法可创建发起方将使用生成的 CHAP 目标的质询响应的共享的机密。

**SetCHAPSharedSecret** WMI 方法属于未发布[MSiSCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关参数的说明**SetCHAPSharedSecret**方法，请参阅成员的说明[ **SetCHAPSharedSecret\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setchapsharedsecret_in)和[**SetCHAPSharedSecret\_出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setchapsharedsecret_out)结构。

微型端口驱动程序实现 MSiSCSI\_操作 WMI 类不支持所需**SetCHAPSharedSecret**。

 

 





