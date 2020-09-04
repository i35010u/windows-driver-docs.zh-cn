---
title: SDEL 中的设备关系令牌
description: 描述可用于在 SDEL 内表示设备关系的令牌的表
ms.assetid: A99d68D2-31A2-99B5-841F-A8249539A39F
keywords:
- 令牌
- 设备关系
ms.date: 09/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: dc678655fec97d7c41c0607ec1d97ebea17254ed
ms.sourcegitcommit: bd72676caf2bf5c9738c4081c778316919b85d30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89456645"
---
# <a name="device-relation-tokens-in-sdel"></a>SDEL 中的设备关系令牌

下表描述了可用于表示 SDEL 中设备关系的标记。 所有这些关系都包含带有 "-或-self" 后缀的版本。 这些 "-或-self" 版本返回当前设备和所有指定的相关设备。

|关系标记|可能的结果|说明|
|----|----|----|
|上述|0到多个|提供以某种方式映射到上述所有设备的方法。 目前，此关系在逻辑上等同于 "disk/self/祖先/OR 祖先////////////"。|
|祖先 (ancestor)|0到多个|扩展父关系，使其包含所有父项，包括 RootDevice。|
|在线订购|0到多个|以某种方式提供到下面的所有设备的映射。 目前，此关系在逻辑上等效于 "子代/卷////或卷/后代-或/或"。|
|子级|0到多个|提供通常在设备与其总线或集线器之间找到的依赖关系。 此关系也称为 "总线关系"。 请注意，虚拟设备不能有子项。|
|descendant|0到多个|将子关系扩展为包含所有子级的所有子级，并将其添加到层次结构的末尾。|
|disk|0到多个|提供从卷设备到实现这些卷的磁盘的映射。 请注意，卷可以跨多个磁盘。|
|父级 (parent)|0 或 1|描述通常在设备与其总线或集线器之间找到的 supremacy 关系。 每个设备都有一个父节点，但逻辑设备除外，它位于 IWDTFDeviceDepot2：： RootDevice 属性中。|
|power|0 或 1|具有与此设备的电源关系的所有设备。  (CM_GETIDLIST_FILTER_POWERRELATIONS) |
|删除|0到多个|介绍 MSDN 的 Microsoft Windows SDK 文档中的 Configuration Manager Api (CM API) 中所述的删除关系。 当删除当前设备时，将删除此关系指定的设备。 只有少数设备具有这种关系。|
|system|1|将任何目标设备对象映射到包含该设备的目标系统对象。 每个设备正好映射到一个系统目标。|
|卷|0到多个|提供从磁盘设备到磁盘公开的卷的映射。 磁盘可以划分为多个卷。|
