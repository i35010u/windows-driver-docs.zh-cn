---
title: INF FeatureScore 指令
description: FeatureScore 指令基于驱动程序支持的功能为驱动程序提供附加排名标准。
keywords:
- INF FeatureScore 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF FeatureScore Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b776f4b757d2a8b153706d7261b66d25b33768d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813107"
---
# <a name="inf-featurescore-directive"></a>INF FeatureScore 指令


**FeatureScore** 指令基于驱动程序支持的功能为驱动程序提供附加排名标准。 例如，可能会为 [设备安装程序类](./overview-of-device-setup-classes.md) 定义功能分数，以区分基于类特定条件的驱动程序。

```inf
[DDInstall]
  
FeatureScore=featurescore
```

Windows Vista 和更高版本的 Windows 支持 **FeatureScore** 指令。

**警告** 仅当直接在 **\[ \] DDInstall** 节中指定时才处理 **FeatureScore** 指令。

 

## <a name="entries"></a>项


<a href="" id="featurescore"></a>*featurescore*  
此值根据驱动程序的功能内容指定该驱动程序的排名分数。 此条目是介于0x00 和0xFF 之间的单字节十六进制数。

较低的 *featurescore* 值指定更好的功能分数排名，其中0x00 是最佳的功能分数排名。 如果未指定 **FeatureScore** 指令，Windows 将对驱动程序使用默认功能评分排名。

<a name="remarks"></a>备注
-------

如果 Windows 为同一设备检测到多个驱动程序，则必须首先确定哪个驱动程序是安装的最佳驱动程序。 为实现此目的，Windows 会根据几个因素或分数为每个驱动程序分配一个总体排名，如下所示：

-   根据驱动程序是否已签名，驱动程序签名分数 () 的 [*签名分数*](signature-score--windows-vista-and-later-.md) 。
-   驱动程序功能分数 ([*功能分数*](feature-score--windows-vista-and-later-.md)) ，具体取决于驱动程序的功能排名与设备的另一驱动程序相比。
-   硬件标识符分数 ([*标识符分数*](identifier-score--windows-vista-and-later-.md)) ，具体取决于即插即用 (PnP) 设备的总线驱动程序报告的设备标识字符串与 inf 文件的 inf [ * **模型** _](inf-models-section.md)部分中的 [设备标识字符串](device-identification-strings.md)匹配。

功能分数提供了一种基于驱动程序支持的功能对驱动程序进行排序的方法。 例如，可能会为 [设备安装程序类](./overview-of-device-setup-classes.md) 定义功能分数，以便根据特定于类的条件来区分驱动程序。

功能分数对标识符分数进行了补充，这使得驱动程序编写者可以更轻松、更准确地区分设备上基于定义完善的条件的不同驱动程序。

有关如何对驱动程序进行排序的详细信息，请参阅 [windows (Windows Vista 和更高版本) 的驱动程序的方式 ](how-setup-ranks-drivers--windows-vista-and-later-.md)。

## <a name="see-also"></a>请参阅


[功能分数](feature-score--windows-vista-and-later-.md)

[标识符分数](identifier-score--windows-vista-and-later-.md)

[_ *_模型_**](inf-models-section.md)

[签名分数](signature-score--windows-vista-and-later-.md)

 

