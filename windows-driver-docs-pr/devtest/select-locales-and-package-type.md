---
title: 在设备元数据创作向导中选择区域设置和包类型
description: 在设备元数据创作向导中选择区域设置和包类型
keywords:
- 在设备元数据创作向导中选择区域设置和包类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef085db568a5400b33c36fc757323ecd56ef421
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834657"
---
# <a name="select-locales-and-package-type-in-the-device-metadata-authoring-wizard"></a>在设备元数据创作向导中选择区域设置和包类型


若要开始，请选择相应的元数据包的区域设置或区域设置，以及 (Windows 7 或 Windows 8) 的包类型。

### <a name="span-idto_set_locale_and_package_typespanspan-idto_set_locale_and_package_typespanspan-idto_set_locale_and_package_typespanto-set-locale-and-package-type"></a><span id="To_set_locale_and_package_type"></span><span id="to_set_locale_and_package_type"></span><span id="TO_SET_LOCALE_AND_PACKAGE_TYPE"></span>设置区域设置和包类型

1.  单击 " **包定义** " 选项卡。
2.  在 " **可用区域设置**" 下，选择要与元数据包关联的区域设置。
    **注意**  
    所有元包都需要此步骤。

    对于 Windows 7 包，该工具会创建多个单区域设置设备元数据包。 对于 Windows 8，它会创建包含多个区域设置的单个元数据包。



3.  在 " **区域设置默认值**" 下，执行以下操作之一：
    -   如果希望包在无法用于区域设置时以特定语言显示，请选择所需的语言。
        **注意**  只能将一个元数据包指定为本地默认包。




-   如果你不希望包在特定于区域设置的包不可用时以特定语言显示，请选择 " **无默认值**"。


4.  在屏幕底部，选择以下选项中的一个或两个：
    -   如果满足以下条件，请选择 " **Windows 8 包 (每个包的多个区域设置)** ：
        -   可以在任何显示语言中使用 "**控制面板**" 的 "Windows 7 **设备和打印机**" 中的默认设备信息 (例如，所有显示语言) 的英语资源。
        -   需要减少设备元数据包的数量。
    -   如果满足以下条件，请选择 " **Windows 7 样式设备元数据包 (每个包的区域设置)** ：
        -   不能在给定语言的元数据包中包含另一种语言的信息。
        -   需要在 **"控制面板**" 中的 "**设备和打印机**" 中区分区域设置。









