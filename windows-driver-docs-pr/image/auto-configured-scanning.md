---
title: 自动配置的扫描
description: 自动配置的扫描
ms.assetid: 6904e216-3eb7-419f-a6ca-198defaeebe0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 196e56d6b468014450c3d12279a88e05459d5c2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373351"
---
# <a name="auto-configured-scanning"></a>自动配置的扫描


在 Windows 7 和更高版本，可支持 WIA 微型驱动程序*自动配置扫描*。 WIA 扫描程序设备，实现自动配置扫描可以自动配置其设备设置响应的扫描作业，设备状态的更改和对用户操作的要求。 而无需执行自动配置扫描的功能，设备必须通常依赖于在桌面计算机上运行的 WIA 应用程序配置的设置。

自动配置扫描提供了适用于 WIA 扫描程序设备执行 WIA 应用程序可能无法执行的特定于设备的优化机会。

此外，自动配置扫描可以减轻 WIA 应用程序负责决定如何配置所选输入的源 （平板、 自动文档送纸器或电影扫描适配器） 扫描操作。 支持推送扫描 （也称为由设备发起扫描） 的设备使用户能够启动设备，而不是从应用程序的用户界面中的扫描操作。 通常情况下，如果设备执行推送扫描，并且具有多个输入源，用户希望能够从设备选择扫描操作的输入的源。 若要避免配置所选的输入的源的任务，该应用程序可用于自动配置扫描来卸载到设备的此任务。

WIA 2.0 微型驱动程序可以支持自动配置所有类型的 WIA 扫描程序设备，包括连接到串行和并行端口、 连接到 USB、 SCSI、 和 IEEE 1394 总线的扫描仪和已连接网络的 Web 服务扫描程序的扫描程序都扫描。

在 Windows Vista 中，Microsoft Web Services for Devices (WSD) 扫描类驱动程序包括一个自定义驱动程序扩展插件以支持自动配置扫描。 此驱动程序提供了自动配置扫描仅为实现 Windows 设备协议 (WDP) 1.0 的扫描仪的网络 WIA 扫描程序设备。 在 Windows 7 中，WSD 扫描类驱动程序实现自动配置扫描中前面段落所述的标准功能，而不作为自定义驱动程序扩展。 有关 WSD 扫描类驱动程序的详细信息，请参阅[与适用于设备的 Web 服务的 WIA](wia-with-web-services-for-devices.md)。 有关扫描程序 WDP 的详细信息，请参阅[Web 服务的设备扫描服务架构](https://msdn.microsoft.com/library/windows/hardware/ff547963)。

### <a name="examples"></a>示例

为了举例说明自动配置扫描，WIA 扫描程序设备可能具有平板和自动文档送纸器。 如果用户将文档放在送纸器中，设备检测到的输入源的隐式选择，它会自动扫描从此源在用户按开始扫描按钮时。 基于所选的输入源，设备可以自动自身配置为使用适用于源的扫描设置。 此外，设备可能有一个通过该用户可以选择在设备自动配置，而无需干预的应用程序的设置的前面板。

具有一个输入源 （例如，平板） 的 WIA 扫描程序设备还可以使用自动配置扫描。 设备可自动配置基于扫描作业，要求其扫描设置，或设备可以应用用户从设备的前面板中选择的设置。

本部分包含以下主题：

[自动项](auto-item.md)

[支持的自动项 WIA 属性](wia-properties-supported-by-an-auto-item.md)

 

 




