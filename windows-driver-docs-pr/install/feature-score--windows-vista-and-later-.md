---
title: 功能分数
description: 功能分数
ms.assetid: cc7f2cd1-85aa-43be-9c4e-abdba3a4310a
keywords:
- 功能分数 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e3a5daa004035d7a1734ce6406757403887eb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360616"
---
# <a name="feature-score"></a>功能分数


驱动程序级别的格式设置为 0x*SSGGTHHH*，其中值 0x*SS*000000 是[签名分数](signature-score--windows-vista-and-later-.md)，值 0x00*GG*0000 是功能得分和 0x0000 值*THHH*是[标识符分数](identifier-score--windows-vista-and-later-.md)。

特征评分提供排名基于驱动程序支持的功能的驱动程序的方法。 例如，可能会为定义特征评分[设备安装程序类](device-setup-classes.md)的区分特定于类的条件的驱动程序。 特征评分对标识符分数，从而可以更轻松、 准确地说是区分不同的驱动程序基于明确定义的条件的设备驱动程序编写者进行了补充。

Microsoft 定义特定设备类的功能分数使用的情况。 特征评分不是必需的众多设备类不具有指定功能分数用法。 在这种情况下，默认功能分数 (0xFF) 预期行为，并将驱动程序的 INF 中定义特征评分没有分配。

当 Microsoft 明确不要求设备类的特征评分时，驱动程序应该：

-   不在驱动程序 INF 中定义特征评分 （Windows 将默认为 0xFF）

    或

-   在驱动程序 INF 中显式定义 0xFF 特征评分

设置驱动程序的功能得分[ **INF FeatureScore 指令**](inf-featurescore-directive.md)中[ **INF DDInstall 部分**](inf-ddinstall-section.md)的 INF 文件安装设备。 特征评分设置，如下所示：

```cpp
[DDInstallSectionName]
. . .
FeatureScore=featurescore
```

其中*DDInstallSectionName*的名称*DDInstall*部分并*featurescore*是 0x00 到 0xFF 之间的单字节十六进制数字。 Windows 计算基于的驱动程序的功能分数*featurescore*的值**FeatureScore**指令：

```cpp
feature score = (featurescore * 0x10000)
```

如果[ **INF FeatureScore 指令**](inf-featurescore-directive.md) INF 文件，Windows 使用默认功能分数是驱动程序指示没有首选项的功能的基于 0x00FF0000 中未指定驱动程序。 越低功能分数，更好的排名，其中的最佳功能分数是 0x00000000。

例如，以下设置驱动程序的功能得分为 0x00FD0000:

```cpp
[DDInstallSectionName]
. . .
FeatureScore=xFD
```

有关驱动程序分级的详细信息，请参阅[如何 Windows Ranks Drivers](how-setup-ranks-drivers--windows-vista-and-later-.md)。

 

 





