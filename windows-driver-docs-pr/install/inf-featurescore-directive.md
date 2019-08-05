---
title: INF FeatureScore 指令
description: FeatureScore 指令提供其他排名条件用于驱动程序基于驱动程序支持的功能。
ms.assetid: 78e1c2cf-b3e9-43ea-b435-979360cc3e28
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
ms.openlocfilehash: 1263574f3266e452e0970eb90e095d1a453a2737
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356998"
---
# <a name="inf-featurescore-directive"></a>INF FeatureScore 指令


**FeatureScore**指令提供的其他排名条件基于驱动程序支持的功能的驱动程序。 例如，可能会为定义特征评分[设备安装程序类](device-setup-classes.md)的区分基于特定于类的条件的驱动程序。

```ini
[DDInstall]
  
FeatureScore=featurescore
```

**FeatureScore**指令支持 Windows Vista 和更高版本的 Windows 中。

**警告**   **FeatureScore**中直接指定时，只处理指令 **\[DDInstall\]** 部分。

 

## <a name="entries"></a>条目


<a href="" id="featurescore"></a>*featurescore*  
此值指定基于其功能内容的驱动程序的排名分数。 此项是 0x00 到 0xFF 之间的单字节十六进制数字。

较低*featurescore*值指定更好的功能分数排名，其中 0x00 是最佳功能分数排名。 如果**FeatureScore**指令未指定，Windows 驱动程序将使用默认功能分数排名为 0xFF。

<a name="remarks"></a>备注
-------

如果 Windows 检测到同一设备的多个驱动程序，必须首先确定哪个驱动程序是最适合的驱动程序安装。 若要实现此目的，Windows 将每个驱动程序分配总排名基于多个因素或评分，如下所示：

-   驱动程序签名的分数 ([*签名分数*](signature-score--windows-vista-and-later-.md) )，根据该驱动程序进行签名。
-   驱动程序功能分数 ([*功能分数*](feature-score--windows-vista-and-later-.md))，根据如何驱动程序的功能级别相比到另一个设备驱动程序。
-   硬件标识符分数 ([*标识符分数*](identifier-score--windows-vista-and-later-.md))，基于紧密程度插 (PnP) 设备标识字符串，为其报告由总线驱动程序的设备匹配[设备标识字符串](device-identification-strings.md)在 INF [***模型***](inf-models-section.md) INF 文件部分。

特征评分提供排名基于驱动程序支持的功能的驱动程序的方法。 例如，可能会为定义特征评分[设备安装程序类](device-setup-classes.md)的区分特定于类的条件的驱动程序。

特征评分对标识符分数，这样就可以更轻松、 准确地说是区分不同的驱动程序基于明确定义的条件的设备驱动程序编写者进行了补充。

有关如何进行排名的驱动程序的详细信息，请参阅[如何 Windows Ranks Drivers （Windows Vista 和更高版本）](how-setup-ranks-drivers--windows-vista-and-later-.md)。

## <a name="see-also"></a>请参阅


[特征评分](feature-score--windows-vista-and-later-.md)

[标识符分数](identifier-score--windows-vista-and-later-.md)

[***模型***](inf-models-section.md)

[签名分数](signature-score--windows-vista-and-later-.md)

 

 






