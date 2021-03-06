---
title: Windows 5G MBIM 接口
description: Windows 5G MBIM 接口
keywords:
- Windows 5G MBIM 接口
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6cb8ceef99839980153520d85a597978bcd71d26
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250425"
---
# <a name="windows-5g-mbim-interface"></a>Windows 5G MBIM 接口

从 Windows 10 版本1903，整个中的5G 仍在开发中。 从网络部署的角度来看，5G 应分两个阶段进行部署： 

* 在阶段1中，大多数移动网络操作员都应该部署5G，并将5G 广播添加到现有的 LTE 广播和 EPC 核心部署（通常称为 "nonstandalone 5G" 网络）。  

* 在阶段2中，移动网络操作员应并行替换 Epc 和 NGCs，并 densify 5G 无线电部署，以启用真正的 "独立" 或基于 NR 的5G 网络。 阶段2接口扩展不在本主题或 Windows 版本的范围内。 

Windows 10 版本1903中引入了用于支持基本阶段1网络要求或基于 EPC 的 nonstandalone 5G 网络的接口扩展。 为了能够实现与旧的调制解调器的可扩展且完全向后兼容，引入了新的 Microsoft MBIM 扩展版本 (2.0) 。 

新的 Microsoft MBIM 扩展版本是必需的，因为 [MBIM 1.0 勘误表规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip) 包含用于添加和播发可选 cid 的机制，但它缺少一种机制来更改现有 cid (新负载或修改的负载) 或引入可选 cid 无法提供的任何方面的更改。 每个有效负载可能由固定大小的成员或动态大小 () 成员的偏移/大小对组成。 如果存在一个或多个动态大小的成员，则最后一个成员的大小为 variable。  

此规范还为主机添加了一个新的 CID，以将其 MBIM 发行版和扩展发行版播发到 MBIM 设备。 对于字段中已存在的旧驱动程序，此 CID 是可选的，因此完全维护向后兼容性。  有关更多详细信息，请参阅 [MBIMEx 2.0 – 5G NSA 支持](mbimex-2.0-5g-nsa-support.md)。 