---
title: VF 微型端口驱动程序的 INF 要求
description: VF 微型端口驱动程序的 INF 要求
ms.assetid: D15B337F-EC63-4E9A-94DA-E7F0487D5D48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8689e6415e710b2d6a7ae6fce9022283dbe493c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327708"
---
# <a name="inf-requirements-for-vf-miniport-drivers"></a>VF 微型端口驱动程序的 INF 要求


微型端口驱动程序的 PCI Express (PCIe) 虚拟函数 (VF) 的 INF 文件未指定任何单个根 I/O 虚拟化 (SR-IOV) 的标准化的 INF 关键字。 只有 INF 文件的 PCIe 物理函数 (PF) 指定标准化的 SR-IOV 关键字。 有关这些关键字的详细信息，请参阅[PF 微型端口驱动程序的 INF 要求](inf-requirements-for-pf-miniport-drivers.md)。

VF 微型端口驱动程序的 INF 遵循与其他网络适配器的 INF 文件相同的要求 （有一个例外）。 有关详细信息，请参阅[网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

唯一的例外是 VF 微型端口驱动程序的 INF 文件必须为管理 SR-IOV 数据路径的服务定义的绑定关系。 需要这些信息来确保网络访问可以故障转移到综合数据路径如果 VF 数据路径，则将调用出于任何原因。 有关这些数据路径的详细信息，请参阅[SR-IOV 数据路径](sr-iov-data-paths.md)。

若要将绑定到管理这些数据路径的服务，VF 微型端口驱动程序的 INF 文件必须指定以下设置以用于**UpperRange**并**LowerRange**条目：

``` syntax
HKR, Ndi\Interfaces, UpperRange, 0, "ndisvf"
HKR, Ndi\Interfaces, LowerRange, 0, "iovvf"
```

 

 





