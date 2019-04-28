---
title: 将 Windows 配置为对驱动程序签名进行平等的分级
description: 将 Windows 配置为对驱动程序签名进行平等的分级
ms.assetid: 727ad66d-b8f3-4e22-b51f-af9571ae0ec8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6afc27ab997232703ecea67a4cd01e8b1dfc4d3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346847"
---
# <a name="configuring-windows-to-rank-driver-signatures-equally"></a>将 Windows 配置为对驱动程序签名进行平等的分级


[AllSignersEqual 组策略](allsignersequal-group-policy--windows-vista-and-later-.md)控件[Windows 驱动程序的级别](how-setup-ranks-drivers.md)与第三方供应商签名的驱动程序由 Microsoft 签名。 启用 AllSignersEqual 组策略后，Windows 就会查看所有 Microsoft 签名类型和秩等于作为第三方签名时它将选择最匹配的设备的驱动程序。

**请注意**  在 Windows Vista 和 Windows Server 2008 **AllSignersEqual**组策略在默认情况下处于禁用状态。 从 Windows 7 开始，默认情况下启用此组策略。

 

启用 AllSignersEqual 组策略后，此配置更改适用于所有后续的驱动程序安装在目标系统上，直到你禁用 AllSignersEqual 组策略。

有关如何配置详细信息**AllSignersEqual**同样，请参阅组策略应用到排名驱动程序签名[AllSignersEqual 组策略 （Windows Vista 和更高版本）](allsignersequal-group-policy--windows-vista-and-later-.md)。

 

 





