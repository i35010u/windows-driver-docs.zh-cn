---
title: 探测和锁定配置
description: 探测和锁定配置
keywords:
- 视频解码 WDK DirectX VA，配置探测和锁定
- 解码视频 WDK DirectX VA，配置探测和锁定
- 图片解码 WDK DirectX VA，配置探测和锁定
- 最小互操作性配置集 WDK DirectX VA
- 锁定配置 WDK DirectX VA
- 探测配置 WDK DirectX VA
- 配置探测和锁定 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba87dd20428824a50e3d24b51a0d743b55504d62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840751"
---
# <a name="probing-and-locking-of-configurations"></a>探测和锁定配置


## <span id="ddk_probing_and_locking_of_configurations_gg"></span><span id="DDK_PROBING_AND_LOCKING_OF_CONFIGURATIONS_GG"></span>


为每个 DirectX VA 函数建立配置的过程 (了需要 (配置的特定值 [bDXVA \_ Func](bdxva-func-variable.md)) 例如，压缩的图片解码、alpha 混合数据加载和 alpha 混合组合) 可以通过以下方式执行：

1.  如果需要，请) 探查 (，以确定快捷键是否接受配置。

2.  锁定特定配置（如果支持）。

若要确定是否支持特定的配置，请将探测命令发送到要探测的特定 *bDXVA \_ Func* 值的快捷键，以及配置。 除了探测命令外，还会发送 *bDXVA \_ Func*) 中值的配置结构，该 (结构描述了所探测的配置以确定是否支持配置。 然后，加速器返回值 \_ "true" 或 " \_ FALSE"，指示快捷键是否支持指定的配置。 此加速器还可以返回建议的备用配置。

若要锁定特定的配置，请将锁定命令发送到快捷键，以使特定的 *bDXVA \_ Func* 被锁定。 对于 "锁定" 命令，将发送 *bDXVA \_ Func*) 中值的配置 (结构，用于描述要在配置中锁定的配置（如果支持配置）。 加速器返回一个 \_ "正常" 或 " \_ FALSE"，指示加速器是否支持指定的配置。 如果返回值为 \_ "确定"，则会锁定指定的配置以供使用。 如果返回值为 S \_ FALSE，则返回建议的备用配置。

解码器可能会在不首先发送针对指定配置的探测命令的情况下发送锁定命令。 如果加速器 \_ 在特定配置的探测命令中返回 "ok"，则它会将 \_ "ok" 返回给相同配置的锁定命令，除非另有说明。 在发送了锁定命令并且加速器返回 S \_ OK 后，指定的配置将被锁定，并且解码器将不会为相同值的 *bDXVA \_ Func* 发送额外的探测或锁定命令。

为了确保所有 DirectX VA 软件解码器都可以使用所有 DirectX VA 加速器操作， [最小互操作性配置集](minimal-interoperability-configuration-sets.md) 定义为一组配置，任何解码器都必须使用 *bDXVA \_ Func* 的特定值来支持这些配置。 通过公开关联的视频加速器 GUID 来指示支持 *bDXVA \_ Func* 变量的每个快捷键必须至少支持此互操作性配置集的一个成员。 在某些情况下，还可以定义 [另一个鼓励配置集](additional-encouraged-configuration-set.md) 。

下图显示解码器发送的探测和锁定命令的控制流。

![演示探测和锁定以设置驱动程序配置的流程图](images/probe-lock.png)

 

 





