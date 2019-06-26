---
title: 控件面板向导替换
description: 控件面板向导替换
ms.assetid: d4a418b6-a9f9-41c4-99a9-20992abe80e9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90106dfc29bcfc450c08eeaa88346affdf5976a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381835"
---
# <a name="control-panel-wizard-replacement"></a>控件面板向导替换





默认 UI 扫描仪和照相机向导 （可从控制面板、 扫描仪和照相机），驱动程序的图标双击时将显示而不是供应商 UI。 此向导不是可替换使用相同的机制作为通用对话框。 它是可以显示你在控制面板中的供应商 UI。

若要显示在控制面板中你将需要在供应商 UI:

-   将你获取的应用程序注册为其设备的默认持久性的事件处理程序。

-   编写自定义向导。

没有任何关系在所有自定义向导和对话框中使用替换[ **IWiaUIExtension::DeviceDialog** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))接口。 但是，请小心。 在控制面板中的图标将始终默认为 Windows Me 和 Windows XP 中的向导。 用户需要右键单击并选择扫描显式以显示默认 WIA\_事件\_扫描\_映像事件处理程序。 在我的电脑，反过来也成立;无论您选择的默认处理程序将是用户双击设备图标上时使用。

 

 




