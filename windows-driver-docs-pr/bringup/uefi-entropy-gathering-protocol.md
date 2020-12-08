---
title: UEFI 熵收集协议
description: UEFI 平均数量收集协议用于以众所周知的方式生成随机数生成 (RNG) 值。
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1504f50e4a4d309deb44a7d51901552b619adafb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783573"
---
# <a name="uefi-entropy-gathering-protocol"></a>UEFI 熵收集协议

UEFI 平均数量收集协议用于以众所周知的方式生成随机数生成 (RNG) 值。

实现此协议的 UEFI RNG 服务采用一个可选输入值，用于标识 RNG 算法，并基于输入值和内部状态提供一个 RNG 值，包括其熵源的状态。 如果在原始熵源的输出中使用确定性随机位生成器 (DRBG) ，则其安全级别必须至少为256位。

有关创建此协议中使用的 RNG 值的标准方法的指导，请参阅 [NIST SP 800-90A Rev。 1-建议使用确定性随机位生成器进行随机数生成](https://csrc.nist.gov/publications/detail/sp/800-90a/rev-1/final)。

## <a name="protocol-interface"></a>协议接口

- [EFI \_ RNG \_ 服务 \_ 绑定 \_ 协议](efi-rng-service-binding-protocol.md)

- [EFI \_ RNG \_ 协议](efi-rng-protocol.md)

- [**EFI \_ RNG \_ 算法 \_ 列表**](efi-rng-algorithm-list.md)
