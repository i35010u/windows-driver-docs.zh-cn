---
Description: 支持的方案
title: 支持的方案
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1464cc6eb3bc4b10b66ed900a61a328efaa4647
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380858"
---
# <a name="supported-scenarios"></a>支持的方案


设备内容、 控制设备行为和要启用垂直解决方案，可传输到或从设备的内容浏览 Windows 便携式设备 (WPD) DDI。 本部分介绍每种方案。

## <a name="span-idcontenttransferspanspan-idcontenttransferspanspan-idcontenttransferspancontent-transfer"></a><span id="Content_Transfer"></span><span id="content_transfer"></span><span id="CONTENT_TRANSFER"></span>内容传输


WPD 提供必要的基础结构进行标准化的应用程序和连接到运行 Windows 的计算机的便携设备之间的数据传输。 它提供了应用程序与设备和其内容，以及标准化的机制来访问和传输数据的统一视图。

例如，WPD DDI 使应用程序可以在设备和计算机之间的内容同步。

## <a name="span-idbrowsingdevicecontentsspanspan-idbrowsingdevicecontentsspanspan-idbrowsingdevicecontentsspanbrowsing-device-contents"></a><span id="Browsing_Device_Contents"></span><span id="browsing_device_contents"></span><span id="BROWSING_DEVICE_CONTENTS"></span>浏览设备内容


通过使用 WPD 命名空间，用户可以对任何类型的可移植设备应用 Windows 文件管理方法。 (有关如何在 WPD 应用程序中实现属性页和上下文菜单扩展的详细信息，请参阅 Windows 便携式设备编程中的指南[WPD SDK](https://go.microsoft.com/fwlink/p/?linkid=178695)。)

## <a name="span-iddevicecontrolspanspan-iddevicecontrolspanspan-iddevicecontrolspandevice-control"></a><span id="Device_Control"></span><span id="device_control"></span><span id="DEVICE_CONTROL"></span>设备控制


除了提供标准设备内容的访问权限，WPD 基础结构提供了以标准化设备控件的方法。 这允许应用程序控制各种设备行为，以及发出设备命令。 例如，适用于移动电话的 WPD 应用程序可以请求电话发送消息或接收消息时连接到计算机。

## <a name="span-idenablingverticalsolutionsspanspan-idenablingverticalsolutionsspanspan-idenablingverticalsolutionsspanenabling-vertical-solutions"></a><span id="Enabling_Vertical_Solutions"></span><span id="enabling_vertical_solutions"></span><span id="ENABLING_VERTICAL_SOLUTIONS"></span>启用垂直解决方案


WPD 基础结构提供高度可扩展的设备的表示形式和控制机制。 这使垂直解决方案提供商使用 WPD 应用程序编程接口 (API) 来创建标准化 WPD 外部设置的增强型的用户体验。 此示例包括设备、 固件更新和设备 （适用于远程支持） 的诊断程序附带的供应商提供软件套件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





