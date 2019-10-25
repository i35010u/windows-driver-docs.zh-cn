---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.assetid: d1f1d6f2-154e-4e41-8ebf-4071de4ceafe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e53529e1e7095f638e5c4f208d967324e617bcc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845043"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret**方法会建立共享机密，以便在验证目标对发起方质询的响应时使用该共享机密。

发起程序使用两个不同的共享机密来实现质询握手身份验证协议（CHAP）：

-   **SetCHAPSharedSecret**方法建立共享机密，发起方使用该共享机密来验证目标对发起方质询的响应。

-   [LoginToTarget](logintotarget.md)方法建立一个共享机密，发起方使用该共享机密来生成针对目标质询的 CHAP 响应。

**SetCHAPSharedSecret** wmi 方法属于未发布的[MSISCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关**SetCHAPSharedSecret**方法的参数的说明，请参阅[**SetCHAPSharedSecret\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_in)和[**SetCHAPSharedSecret\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_out)结构的成员说明。

实现 MSiSCSI\_操作 WMI 类的微型端口驱动程序不需要支持**SetCHAPSharedSecret**。

 

 





