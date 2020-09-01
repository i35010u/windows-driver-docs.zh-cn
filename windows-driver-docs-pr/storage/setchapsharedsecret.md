---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.assetid: d1f1d6f2-154e-4e41-8ebf-4071de4ceafe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b4b8fd68ee33a4bc7ba1b0cdc2381788019875d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189677"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret**方法会建立共享机密，以便在验证目标对发起方质询的响应时使用该共享机密。

发起方使用两个不同的共享机密来实现质询握手身份验证协议 (CHAP) ：

-   **SetCHAPSharedSecret**方法建立共享机密，发起方使用该共享机密来验证目标对发起方质询的响应。

-   [LoginToTarget](logintotarget.md)方法建立一个共享机密，发起方使用该共享机密来生成针对目标质询的 CHAP 响应。

**SetCHAPSharedSecret** wmi 方法属于未发布的[MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关 **SetCHAPSharedSecret** 方法的参数的说明，请参阅 [**SetCHAPSharedSecret \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_in) 和 [**SetCHAPSharedSecret \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_out) 结构的成员说明。

实现 MSiSCSI 操作 WMI 类的微型端口驱动程序 \_ 不需要支持 **SetCHAPSharedSecret**。

 

