---
title: 功能分数
description: 功能分数
keywords:
- 功能分数 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fa7de98fbfed322cc95dfdd658a97be92fa0752
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799483"
---
# <a name="feature-score"></a>功能分数


驱动程序级别的格式设置为 0x *SSGGTHHH*，其中 0x *SS* 000000 的值是 [签名分数](signature-score--windows-vista-and-later-.md)，0x00 *GG* 0000 的值是功能分数，0x0000 *THHH* 的值是 [标识符分数](identifier-score--windows-vista-and-later-.md)。

功能分数提供了一种基于驱动程序支持的功能对驱动程序进行排序的方法。 例如，可能会为 [设备安装程序类](./overview-of-device-setup-classes.md) 定义功能分数，以便根据特定于类的条件来区分驱动程序。 功能分数对标识符分数进行了补充，使得驱动程序编写者可以更轻松、更准确地区分设备上基于定义完善的条件的不同驱动程序。

Microsoft 定义特定设备类的功能分数使用情况。 功能分数并不是必需的，因此许多设备类将不会使用指定的功能分数。 在这种情况下，默认功能分数应 (0xFF) ，并将在驱动程序的 INF 中没有定义的功能分数的情况下进行分配。

当 Microsoft 没有明确要求设备类的功能分数时，驱动程序应：

-   不在驱动程序 INF 中定义功能分数 (Windows 将默认为 0xFF) 

    或

-   明确定义驱动程序 INF 中0xFF 的功能分数

驱动程序的功能分数是通过安装设备的 INF 文件的 inf [**DDInstall 部分**](inf-ddinstall-section.md)中的 [**inf FeatureScore 指令**](inf-featurescore-directive.md)设置的。 功能分数的设置如下所示：

```cpp
[DDInstallSectionName]
. . .
FeatureScore=featurescore
```

其中， *DDInstallSectionName* 是 *DDInstall* 节的名称， *Featurescore* 是介于0x00 和0xff 之间的单字节十六进制数。 Windows 根据 **featurescore** 指令的 *featurescore* 值计算驱动程序的功能分数：

```cpp
feature score = (featurescore * 0x10000)
```

如果 INF 文件中未指定 [**Inf FeatureScore 指令**](inf-featurescore-directive.md) ，Windows 将使用默认的功能分数为驱动程序0x00FF0000，这表明没有基于驱动程序功能的首选项。 功能分数越低，排名越好，最佳功能分数就是0x00000000。

例如，以下将驱动程序的功能分数设置为0x00FD0000：

```cpp
[DDInstallSectionName]
. . .
FeatureScore=xFD
```

有关驱动程序排名的详细信息，请参阅 [Windows 如何对驱动程序](how-setup-ranks-drivers--windows-vista-and-later-.md)进行排名。

 

