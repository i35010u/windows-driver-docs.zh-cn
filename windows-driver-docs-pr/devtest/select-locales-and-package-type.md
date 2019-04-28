---
title: 在设备元数据创作向导中选择区域设置和包类型
description: 在设备元数据创作向导中选择区域设置和包类型
ms.assetid: 02227FAB-A37F-4B20-AD52-E071C19E8743
keywords:
- 在设备元数据创作向导中选择区域设置和包类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5693c025865ea9f4620b1ecf7861dd9e2584e7d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351357"
---
# <a name="select-locales-and-package-type-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中选择区域设置和包类型


若要开始，请选择相应的区域设置的元数据包，以及你的包类型 （Windows 7 或 Windows 8）。

### <a name="span-idtosetlocaleandpackagetypespanspan-idtosetlocaleandpackagetypespanspan-idtosetlocaleandpackagetypespanto-set-locale-and-package-type"></a><span id="To_set_locale_and_package_type"></span><span id="to_set_locale_and_package_type"></span><span id="TO_SET_LOCALE_AND_PACKAGE_TYPE"></span>若要设置区域设置和包类型

1.  单击**包定义**选项卡。
2.  下**可用的区域设置**，选择你想要将与元数据包相关联。
    **注意**  
    此步骤是必需的元数据的所有包。

    对于 Windows 7 包，该工具将创建多个单区域设置设备元数据包。 对于 Windows 8，它将创建包含多个区域设置的单个元包。



3.  下**区域设置默认**，执行下列操作之一：
    -   如果你想要显示特定的语言包不可用的区域设置时的包，，选择所需的语言。
        **请注意**只能以本地默认包的形式指定一个元数据包。




-   如果不希望将显示在特定语言中可用，请选中，并不特定于区域设置的包的包**无默认值**。


4.  在屏幕的底部，选择一个或两个以下选项：
    -   选择**Windows 8 包 （多个区域设置每个包）** 如果以下条件适用：
        -   可以在 Windows 7 中使用的默认设备信息**设备和打印机**中**控制面板**中任何显示语言 （例如，所有的显示语言的英语资源）。
        -   你想要减少设备元数据包的数量。
    -   选择**Windows 7 样式设备元数据包 （单个区域设置每个包）** 如果以下条件适用：
        -   给定的语言的元数据包中，不能包含另一种语言的信息。
        -   你想要区分每个区域设置中的设备信息**设备和打印机**中**控制面板**。









