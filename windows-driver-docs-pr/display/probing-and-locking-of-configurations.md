---
title: 探测和锁定的配置
description: 探测和锁定的配置
ms.assetid: 6f68db48-ed4b-487c-b425-43c610651c16
keywords:
- 视频解码 WDK DirectX va，因此配置探测和锁定
- 解码视频 WDK DirectX va，因此配置探测和锁定
- 解码 WDK DirectX va，因此配置探测和锁定的图片
- 最小互操作性配置设置 WDK DirectX VA
- 锁定配置 WDK DirectX VA
- 探测配置 WDK DirectX VA
- 配置探测和锁定 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31d21d387fdbfacaab9fbe22cf2043d2f12b8cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542654"
---
# <a name="probing-and-locking-of-configurations"></a>探测和锁定的配置


## <span id="ddk_probing_and_locking_of_configurations_gg"></span><span id="DDK_PROBING_AND_LOCKING_OF_CONFIGURATIONS_GG"></span>


建立每个 DirectX VA 函数的配置的过程 (某个特定值的[bDXVA\_Func](bdxva-func-variable.md)) 需要一个配置 (例如，压缩图片解码，alpha 值混合处理的数据加载、 和可以通过执行 alpha 值混合处理组合）：

1.  探测 （如果需要） 以确定是否通过快捷键接受配置。

2.  锁定在特定配置中，如果它受支持。

若要确定是否支持特定的配置，则将探测命令发送到的特定加速器*bDXVA\_Func*要探测，以及配置值。 除了探测的命令中，配置结构 (中的值*bDXVA\_Func*) 发送的描述正在探测来确定是否支持的配置的配置。 快捷键然后返回值为 S\_确定或 S\_FALSE，指示快捷键是否支持指定的配置。 快捷键还可以返回建议的替代配置。

若要锁定在特定配置中，将锁定命令发送到的特定快捷键*bDXVA\_Func*锁定。 与锁定的命令中，配置结构 (中的值*bDXVA\_Func*) 发送，描述要在中，锁定的配置，如果支持的配置。 快捷键返回一个 S\_确定或 S\_FALSE，指示快捷键是否支持指定的配置。 如果返回值为 S\_用于锁定指定的配置好了。 如果返回值为 S\_为 FALSE，则返回建议的替代配置。

解码器可能会发送锁定命令而无需第一个发送指定的配置的探测命令。 如果快捷键返回一个 S\_确定在特定配置的探测命令，它将返回一个 S\_好到该同一配置下，锁定命令，除非另有说明。 已发送锁定命令和快捷键返回后 S\_好了，指定的配置已被锁定，没有其他探测或锁定命令解码器发送相同的值*bDXVA\_Func*.

以确保所有 DirectX VA 软件解码器可以作用都于使用所有的 DirectX VA 加速器[最小互操作性配置集](minimal-interoperability-configuration-sets.md)定义为一任何的组使用特定解码器必须支持的配置值为*bDXVA\_Func*。 指示支持的每个加速器*bDXVA\_Func*变量通过公开关联的视频加速器 GUID 必须支持此互操作性配置集中的至少一个成员。 在某些情况下，[其他建议的配置集](additional-encouraged-configuration-set.md)还可定义。

下图显示了探测和锁定解码器发送命令的控制流。

![流程图，显示了探测和锁定驱动程序配置设置](images/probe-lock.png)

 

 





