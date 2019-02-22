---
title: 支持的属性集
description: 支持的属性集
ms.assetid: 49a3e3e6-3a09-4202-a2cb-df65806d3336
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，属性将设置
- 流式处理微型驱动程序 WDK Windows 2000 内核，属性设置
- 微型驱动程序 WDK Windows 2000 内核流式处理，属性集
- 属性设置 WDK 流式处理的微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25b00f3143c814c4390bd577864ee6f8d85554ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546344"
---
# <a name="supporting-property-sets"></a>支持的属性集





这两种微型驱动程序作为一个整体，并且单个流可以接收属性的请求。 微型驱动程序提供支持中的属性集中**DevicePropertiesArray**的[ **HW\_流\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff559690)。 每个流提供支持中的属性集中**StreamPropertiesArray**的[ **HW\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff559692)结构该流。

微型驱动程序定义了属性集，它通过处理[ **KSPROPERTY\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff565617)数据结构，又指向的数组[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)结构，一个用于在属性集中的每个属性。 如果**GetSupported** KSPROPERTY 成员\_项**TRUE**、 微型驱动程序支持获取属性数据。 如果**SetSupported** KSPROPERTY 成员\_项**TRUE**、 微型驱动程序支持设置的属性数据。

大多数属性支持请求的类驱动程序会自动处理，使用微型驱动程序的信息提供在 KSPROPERTY\_项结构的属性。 例如，如果类驱动程序将收到 KSPROPERTY\_类型\_BASICSUPPORT 请求，它会在数据类型和值范围中查找**值**KSPROPERTY 成员\_项。 请参阅[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)有关详细信息。 如果微型驱动程序需要对其执行自定义处理的支持请求 （这在很少见），它可能会设置**SupportHandler** KSPROPERTY 成员\_项**TRUE**。 类驱动程序，就好像属性 get 请求，然后处理支持请求。 微型驱动程序可以确定从请求的实际类型**标志**属性标识符的成员。

在类驱动程序获取或设置通过传递的微型驱动程序属性[ **SRB\_获取\_设备\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff568170)或[ **SRB\_设置\_设备\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff568204)微型驱动程序的请求[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)例程。 类驱动程序获取或设置流属性通过传递 SRB\_获取\_流\_属性或 SRB\_设置\_流\_到流的属性请求**StrMiniReceiveStreamControlPacket**例程。

在类驱动程序微型驱动程序与通过其中一个微型驱动程序的回调微型驱动程序从偶尔 assist 代表处理许多属性。 微型驱动程序不在其属性集数组中定义这些属性。 有关如何在类驱动程序处理的说明[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)并[KSPROPSETID\_拓扑](https://msdn.microsoft.com/library/windows/hardware/ff566598)属性集，请参阅[支持多个流](supporting-multiple-streams.md)。

 

 




