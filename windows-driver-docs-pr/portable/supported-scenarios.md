---
description: 支持的方案
title: 支持的方案
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79451a2883a2f883b6af35446801a0b1cc79cb89
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969554"
---
# <a name="supported-scenarios"></a>支持的方案


使用 (WPD) DDI 的 Windows 便携式设备，你可以将内容传输到设备、浏览设备内容、控制设备行为和启用垂直解决方案。 本部分介绍上述每种方案。

## <a name="span-idcontent_transferspanspan-idcontent_transferspanspan-idcontent_transferspancontent-transfer"></a><span id="Content_Transfer"></span><span id="content_transfer"></span><span id="CONTENT_TRANSFER"></span>内容传输


WPD 提供必要的基础结构，用于标准化连接到运行 Windows 的计算机的应用程序和便携式设备之间的数据传输。 它为应用程序提供了一种统一的设备及其内容视图，以及用于访问和传输数据的标准化机制。

例如，WPD DDI 使应用程序能够同步设备与计算机之间的内容。

## <a name="span-idbrowsing_device_contentsspanspan-idbrowsing_device_contentsspanspan-idbrowsing_device_contentsspanbrowsing-device-contents"></a><span id="Browsing_Device_Contents"></span><span id="browsing_device_contents"></span><span id="BROWSING_DEVICE_CONTENTS"></span>浏览设备内容


使用 WPD 命名空间，用户可以将 Windows 文件管理方法应用于任何类型的便携设备。  (有关如何在 WPD 应用程序中实现上下文菜单和属性页扩展的详细信息，请参阅 [WPD SDK](https://go.microsoft.com/fwlink/p/?linkid=178695)中的 Windows 便携设备编程指南。 ) 

## <a name="span-iddevice_controlspanspan-iddevice_controlspanspan-iddevice_controlspandevice-control"></a><span id="Device_Control"></span><span id="device_control"></span><span id="DEVICE_CONTROL"></span>设备控制


除了提供对设备内容的标准访问，WPD 基础结构还提供了对设备控件进行标准化的方法。 这样，应用程序便可以控制各种设备行为以及发出设备命令。 例如，移动电话的 WPD 应用程序可以在连接到计算机时请求手机发送消息或接收消息。

## <a name="span-idenabling_vertical_solutionsspanspan-idenabling_vertical_solutionsspanspan-idenabling_vertical_solutionsspanenabling-vertical-solutions"></a><span id="Enabling_Vertical_Solutions"></span><span id="enabling_vertical_solutions"></span><span id="ENABLING_VERTICAL_SOLUTIONS"></span>启用垂直解决方案


WPD 基础结构提供高度可扩展的设备表示形式和控制机制。 这使得垂直解决方案提供商可以使用 WPD 应用程序编程接口 (API) 来创建 WPD 标准化集以外的增强型用户体验。 这种情况的示例包括供应商提供的软件套件，它们包括在设备、固件更新和设备诊断 (中，用于) 远程支持。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





