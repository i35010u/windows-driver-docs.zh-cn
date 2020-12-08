---
title: VF 微型端口驱动程序的 INF 要求
description: VF 微型端口驱动程序的 INF 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38cef9f54447551f3cbb53e8d621ea0b13d962e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841183"
---
# <a name="inf-requirements-for-vf-miniport-drivers"></a>VF 微型端口驱动程序的 INF 要求


PCI Express (PCIe) 虚函数 () VF 的小型小型使用端口驱动程序的 INF 文件未指定针对单一根 i/o 虚拟化 (SR-IOV) 的任何标准化 INF 关键字。 只有 PCIe 物理功能 (PF) 的 INF 文件指定标准化 SR-IOV 关键字。 有关这些关键字的详细信息，请参阅 [PF 微型端口驱动程序的 INF 要求](inf-requirements-for-pf-miniport-drivers.md)。

VF 微型端口驱动程序的 INF (跟有一个例外，) 与网络适配器的其他 INF 文件相同的要求。 有关详细信息，请参阅 [网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

唯一的例外是，VF 微型端口驱动程序的 INF 文件必须定义与管理 SR-IOV 数据路径的服务之间的绑定关系。 这是为了确保当 VF 数据路径由于任何原因而被破坏时，网络访问可能会故障转移到综合数据路径。 有关这些数据路径的详细信息，请参阅 [Sr-iov 数据路径](sr-iov-data-paths.md)。

若要绑定到管理这些数据路径的服务，VF 微型端口驱动程序的 INF 文件必须为 **UpperRange** 和 **LowerRange** 项指定以下设置：

``` syntax
HKR, Ndi\Interfaces, UpperRange, 0, "ndisvf"
HKR, Ndi\Interfaces, LowerRange, 0, "iovvf"
```

 

 





