---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2dd34cf3643300c8b4757603f3548b16c9d06729
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782101"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret** 方法会建立共享机密，以便在验证目标对发起方质询的响应时使用该共享机密。

发起方使用两个不同的共享机密来实现质询握手身份验证协议 (CHAP) ：

-   **SetCHAPSharedSecret** 方法建立共享机密，发起方使用该共享机密来验证目标对发起方质询的响应。

-   [LoginToTarget](logintotarget.md)方法建立一个共享机密，发起方使用该共享机密来生成针对目标质询的 CHAP 响应。

**SetCHAPSharedSecret** wmi 方法属于未发布的 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关 **SetCHAPSharedSecret** 方法的参数的说明，请参阅 [**SetCHAPSharedSecret \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_in) 和 [**SetCHAPSharedSecret \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_out) 结构的成员说明。

实现 MSiSCSI 操作 WMI 类的微型端口驱动程序 \_ 不需要支持 **SetCHAPSharedSecret**。

 

