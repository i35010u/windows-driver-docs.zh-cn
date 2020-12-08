---
title: 将 Windows 配置为对驱动程序签名进行平等的分级
description: 将 Windows 配置为对驱动程序签名进行平等的分级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bd902754d12859839f6eb7b04326ab816fa3c7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782967"
---
# <a name="configuring-windows-to-rank-driver-signatures-equally"></a>将 Windows 配置为对驱动程序签名进行平等的分级


[AllSignersEqual 组策略](./allsigningequal-group-policy.md)控制 Windows 如何对由第三方供应商签署的 Microsoft 签名的[驱动程序](how-setup-ranks-drivers--windows-vista-and-later-.md)和驱动程序进行排名。 启用 AllSignersEqual 组策略后，Windows 会在选择最匹配设备的驱动程序时，将所有 Microsoft 签名类型和第三方签名视为相等。

**注意**  在 Windows Vista 和 Windows Server 2008 中，默认情况下， **AllSignersEqual** 组策略处于禁用状态。 从 Windows 7 开始，默认情况下会启用此组策略。

 

启用 AllSignersEqual 组策略后，此配置更改将应用到目标系统上所有后续的驱动程序安装，直到你禁用 AllSignersEqual 组策略。

有关如何将 **AllSignersEqual** 组策略配置为平等地对驱动程序签名进行排名的详细信息，请参阅 [AllSignersEqual 组策略 (Windows Vista 和更高版本)](./allsigningequal-group-policy.md)。

 

