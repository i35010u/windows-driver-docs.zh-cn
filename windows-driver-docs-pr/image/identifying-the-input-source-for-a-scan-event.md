---
title: 标识扫描事件的输入源
description: 标识扫描事件的输入源
ms.assetid: aaa0bbf4-6866-45d7-8150-c6a74d6c46c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b047bcfc0c08403b7b272ac514337e2f5ed4f70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363049"
---
# <a name="identifying-the-input-source-for-a-scan-event"></a>标识扫描事件的输入源


一个*推送扫描*操作在用户启动从 WIA 的扫描程序设备而不是从桌面计算机上运行的 WIA 应用程序的用户界面是扫描操作。 当用户在设备上按开始扫描按钮时，该应用程序将接收到扫描事件以通知用户已请求扫描操作。 对此事件作出响应，该应用程序可以在以下两种方式之一执行推送扫描操作：

-   如果设备支持[自动配置扫描](auto-configured-scanning.md)，应用程序可以请求从的数据传输[自动项](auto-item.md)以获取从当前所选的输入源 （平板、 自动的映像文档送纸器或电影扫描适配器）。 在响应中，设备会自动配置其扫描设置 (不包括可以仅由应用程序中所述进行配置的几个属性[WIA 属性支持的自动项](wia-properties-supported-by-an-auto-item.md)) 然后将获取图像。

-   应用程序可以执行将在直接程序控制下的执行扫描操作。 首先，应用程序配置 WIA 项 （平板项、 送纸器项或电影项），表示当前所选的输入的源的属性。 接下来，应用程序获取图像，此项请求数据传输。

有关 WIA 项的详细信息，请参阅[WIA 项类别](wia-item-categories.md)。

扫描事件发生时，应用程序将收到一条通知，包括 WIA 的事件标识符 （GUID 值） 来指定事件的性质。 WIA 微型驱动程序可以将自定义的 WIA 的事件标识符 GUID 分配给某一事件，或微型驱动程序可以使用一种 WIA\_事件\_扫描\_*XXX*标头文件中定义的GUID常量*Wiadef.h*。 有关这些常量的详细信息，请参阅[WIA 事件标识符](https://go.microsoft.com/fwlink/p/?linkid=127716)。

虽然扫描事件 WIA 的事件标识符提供了有关事件的信息，但它没有标识要用于扫描操作的输入的源。 用于自动配置扫描程序不需要此信息。 但是，若要执行一次扫描程序直接控制下的，应用程序必须知道哪个输入要使用的源。 应用程序必须具有从设备获取此信息，如果设备具有多个输入的源，并且用户可以从设备，而不是从应用程序的用户界面中选择的输入的源的方法。 如果从设备中选择的输入的源，用户可以选择源显式 （通过设备的前面板上，按下按钮） 或隐式 （例如，通过将文档插入到在设备上送纸器）。

在 Windows 7 和更高版本的 Windows 中，扫描事件发生时，应用程序可查询 WIA 扫描程序设备 WIA\_DPS\_扫描\_可用\_项属性以确定所选的输入的源设备支持此属性。 WIA\_DPS\_扫描\_可用\_项是在设备的 WIA 项树的根项目的可选属性。 有关此属性的详细信息，请参阅[ **WIA\_DPS\_扫描\_可用\_项**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-scan-available-item)。

在 Windows Vista 中，Web Services for Devices (WSD) 扫描类驱动程序支持 WIA\_DPS\_扫描\_可用\_项属性。 该驱动程序定义此属性 (在名称 WIA\_WSD\_扫描\_可用\_项) 作为自定义驱动程序扩展。 该驱动程序仅支持联网的 WIA 扫描程序的设备实现 Windows 设备协议 (WDP) 1.0 用于扫描程序。 在 Windows 7 中，WSD 扫描类驱动程序实现 WIA\_DPS\_扫描\_可用\_作为标准驱动程序功能，如中所述上一段，而不是作为自定义驱动程序扩展的项属性. 有关 WSD 扫描类驱动程序的详细信息，请参阅[与适用于设备的 Web 服务的 WIA](wia-with-web-services-for-devices.md)。 有关扫描程序 WDP 的详细信息，请参阅[Web 服务的设备扫描服务架构](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)。

 

 




