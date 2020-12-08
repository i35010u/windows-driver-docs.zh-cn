---
title: 自动配置的扫描
description: 自动配置的扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8403fc20ad9fcc45a0091b7f1d47891d906da04c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828727"
---
# <a name="auto-configured-scanning"></a>自动配置的扫描


在 Windows 7 和更高版本中，WIA 微型驱动程序可以支持 *自动配置的扫描*。 实现自动配置扫描的 WIA 扫描器设备可以自动配置其设备设置，以响应扫描作业的要求、设备状态的更改和用户操作。 如果不能执行自动配置的扫描，设备通常必须依赖于在台式计算机上运行的 WIA 应用程序来配置设置。

自动配置的扫描为 WIA 扫描器设备执行 WIA 应用程序可能无法执行的特定于设备的优化提供了机会。

此外，自动配置的扫描可以减轻 WIA 应用程序负责确定如何配置所选输入源 (平板、自动文档送纸器或胶卷扫描适配器) 进行扫描操作。 支持推送扫描 (的设备也称为设备启动的扫描) 使用户能够从设备而不是从应用程序的用户界面启动扫描操作。 通常情况下，如果设备执行推送扫描，并且有多个输入源，用户希望能够从设备中选择扫描操作的输入源。 若要避免配置所选输入源，应用程序可以使用自动配置的扫描将此任务卸载到设备。

WIA 2.0 微型驱动程序可支持对所有类型的 WIA 扫描仪设备进行自动配置的扫描，包括连接到串行和并行端口的扫描程序、连接到 USB、SCSI 和 IEEE 1394 总线的扫描仪以及连接到网络的 Web 服务扫描程序。

在 Windows Vista 中，适用于设备的 Microsoft Web 服务 (WSD) scan 类驱动程序包括自定义驱动程序扩展以支持自动配置的扫描。 此驱动程序只为实现 Windows 设备协议 (WDP) 1.0 for 扫描仪的网络 WIA 扫描器设备提供自动配置的扫描。 在 Windows 7 中，WSD 扫描类驱动程序将自动配置的扫描作为标准功能实现，如前面的段落所述，而不是作为自定义驱动程序扩展。 有关 WSD 扫描类驱动程序的详细信息，请参阅 [WIA With Web Services For Devices](wia-with-web-services-for-devices.md)。 有关 WDP for 扫描仪的详细信息，请参阅 [Web Services For Devices Scan Service Schema](./scan-service--ws-scan--schema.md)。

### <a name="examples"></a>示例

对于自动配置的扫描，WIA 扫描器设备可能同时具有平板和自动进纸器。 如果用户将文档放入送纸器，设备将检测到输入源的隐式选择，当用户按 "开始扫描" 按钮时，它会自动从此源进行扫描。 根据所选的输入源，设备可以自动将自身配置为使用适用于源的扫描设置。 此外，设备可能有一个前面板，用户可以通过该面板选择设备自动配置的设置，而无需应用程序进行干预。

带有一个输入源的 WIA 扫描器设备 (例如，平板) 也可以使用自动配置的扫描。 设备可以根据扫描作业的要求自动配置其扫描设置，或者设备可以应用用户从设备的前面板中选择的设置。

本节包含下列主题：

[自动项](auto-item.md)

[自动项支持的 WIA 属性](wia-properties-supported-by-an-auto-item.md)

 

