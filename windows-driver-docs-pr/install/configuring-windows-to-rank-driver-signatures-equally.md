---
title: 将 Windows 配置为对驱动程序签名进行平等的分级
description: 将 Windows 配置为对驱动程序签名进行平等的分级
ms.assetid: 727ad66d-b8f3-4e22-b51f-af9571ae0ec8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7bb2a3138719b5f0a46d26bc521784a540f84af
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557794"
---
# <a name="configuring-windows-to-rank-driver-signatures-equally"></a>将 Windows 配置为对驱动程序签名进行平等的分级


[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)控制 Windows 如何对由第三方供应商签署的 Microsoft 签名的[驱动程序](how-setup-ranks-drivers--windows-vista-and-later-.md)和驱动程序进行排名。 启用 AllSignersEqual 组策略后，Windows 会在选择最匹配设备的驱动程序时，将所有 Microsoft 签名类型和第三方签名视为相等。

**注意**   在 Windows Vista 和 Windows Server 2008 中，默认情况下， **AllSignersEqual**组策略处于禁用状态。 从 Windows 7 开始，默认情况下会启用此组策略。

 

启用 AllSignersEqual 组策略后，此配置更改将应用到目标系统上所有后续的驱动程序安装，直到你禁用 AllSignersEqual 组策略。

有关如何将**AllSignersEqual**组策略配置为平等地对驱动程序签名进行排序的详细信息，请参阅[AllSignersEqual 组策略（Windows Vista 和更高版本）](allsignersequal-group-policy--windows-vista-and-later-.md)。

 

 





