---
title: UEFI 平均信息量正在收集协议
description: UEFI 平均信息量收集协议用于生成随机数生成 (RNG) 值的已知的方式。
ms.assetid: 616F178F-B4A0-4B8B-B71D-F7474738EA35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ce227750ac8a71300da634487ad586357a5140
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543282"
---
# <a name="uefi-entropy-gathering-protocol"></a>UEFI 平均信息量正在收集协议


UEFI 平均信息量收集协议用于生成随机数生成 (RNG) 值的已知的方式。

实现此协议的 UEFI RNG 服务采用一个可选的输入的值，标识 RNG 算法，并提供基于输入的值和内部状态，包括其平均信息量源状态的 RNG 值。 原始平均信息量源的输出上使用确定性的随机位生成器 (DRBG) 时，其安全级别必须至少 256 位。

有关创建此协议中使用的 RNG 值的标准方法的指南，请参阅[NIST SP 800 90A 建议使用确定性的随机位生成器的随机数字生成]( https://go.microsoft.com/fwlink/p/?LinkId=523737)。

## <a name="protocol-interface"></a>协议接口


-   [EFI\_RNG\_SERVICE\_BINDING\_PROTOCOL](efi-rng-service-binding-protocol.md)

-   [EFI\_RNG\_PROTOCOL](efi-rng-protocol.md)

-   [**EFI\_RNG\_ALGORITHM\_LIST**](efi-rng-algorithm-list.md)

 

 




