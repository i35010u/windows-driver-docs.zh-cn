---
title: 标识扫描事件的输入源
description: 标识扫描事件的输入源
ms.assetid: aaa0bbf4-6866-45d7-8150-c6a74d6c46c1
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: abb2835d5953f464874902b91bb7187d84ff99bf
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223558"
---
# <a name="identifying-the-input-source-for-a-scan-event"></a>标识扫描事件的输入源

*推送扫描*操作是用户从 wia 扫描器设备启动的扫描操作，而不是在台式计算机上运行的 wia 应用程序的用户界面。 当用户按下设备上的 "开始扫描" 按钮时，应用程序会收到 scan 事件，通知用户已请求扫描操作。 为响应此事件，应用程序可以通过以下两种方式之一执行推送扫描操作：

- 如果设备支持[自动配置的扫描](auto-configured-scanning.md)，应用程序可以请求从[自动项](auto-item.md)进行数据传输，以便从当前选择的输入源（平板、自动文档送纸器或胶卷扫描适配器）获取图像。 在响应中，设备将自动配置其扫描设置（不包括只能由应用程序配置的几个属性，这些属性在[自动项支持的 WIA 属性](wia-properties-supported-by-an-auto-item.md)中介绍），然后获取该图像。

- 应用程序可以在 "直接程序控制" 下执行扫描操作。 首先，应用程序配置表示当前选定输入源的 WIA 项（"平板" 项、"送纸器项" 或 "电影" 项）的属性。 接下来，应用程序将通过请求从该项传输数据来获取映像。

有关 WIA 项的详细信息，请参阅[Wia 项类别](wia-item-categories.md)。

发生扫描事件时，应用程序将收到一个通知，其中包含 WIA 事件标识符（GUID 值）以指定事件的性质。 WIA 微型驱动程序可以将自定义 WIA 事件标识符 GUID 分配给事件，或微型驱动程序可以使用 \_ \_ \_ 标头文件*Wiadef*中定义的一个 WIA 事件扫描*XXX* guid 常量。 有关这些常量的详细信息，请参阅[WIA 事件标识符](https://docs.microsoft.com/windows/win32/wia/-wia-wia-event-identifiers)。

尽管 scan 事件的 WIA 事件标识符提供了有关事件的信息，但它并不标识用于扫描操作的输入源。 对于自动配置的扫描，应用程序不需要此信息。 但是，若要在直接程序控制下执行扫描，应用程序必须知道要使用的输入源。 如果设备具有多个输入源，并且用户可以从设备（而不是从应用程序的用户界面）中选择输入源，则该应用程序必须能够从设备获取此信息。 从设备选择输入源时，用户可以显式选择源（通过按设备前面板上的按钮）或隐式选择（例如，通过将文档插入设备上的进纸器）。

发生扫描事件时，如果设备支持此属性，应用程序可以查询 WIA 扫描器设备的 "WIA \_ DPS \_ 扫描 \_ 可用 \_ 项" 属性来确定所选的输入源。 WIA \_ DPS \_ SCAN \_ 可用 \_ 项是设备的 WIA 项树中根项的可选属性。 有关此属性的详细信息，请参阅[**WIA \_ DPS \_ SCAN \_ 可用 \_ 项**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-scan-available-item)。

\_ \_ 由于上一段中所述，WSD 扫描类驱动程序将 WIA DPS scan \_ 可用 \_ 项属性作为标准驱动程序功能实现，而不是作为自定义驱动程序扩展。 有关 WSD 扫描类驱动程序的详细信息，请参阅[WIA With Web Services For Devices](wia-with-web-services-for-devices.md)。 有关 WDP for 扫描仪的详细信息，请参阅[Web Services For Devices Scan Service Schema](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)。
