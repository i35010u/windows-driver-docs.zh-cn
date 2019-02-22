---
title: 定义加速器功能
description: 定义加速器功能
ms.assetid: 1f590cfd-74b8-4a08-848d-fcbb2c0c9486
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，加速器功能
- 视频加速 WDK DirectX，加速器功能
- VA WDK DirectX，加速器功能
- 受限制的配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b6751a906b48c22c4bc989e962a7bc658c4cd37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548014"
---
# <a name="defining-accelerator-capabilities"></a>定义加速器功能


## <span id="ddk_defining_accelerator_capabilities_gg"></span><span id="DDK_DEFINING_ACCELERATOR_CAPABILITIES_GG"></span>


快捷键可在受限制的操作，在这种情况下它符合[受限制的配置文件](restricted-profiles.md)，或可在 nonrestricted 操作中，在这种情况下它不符合受限制的配置文件。

### <a name="span-idrestrictedoperationspanspan-idrestrictedoperationspanspan-idrestrictedoperationspanrestricted-operation"></a><span id="Restricted_Operation"></span><span id="restricted_operation"></span><span id="RESTRICTED_OPERATION"></span>受限制的操作

它支持根据哪个受限制的配置文件定义的快捷键的功能。 加速器可能支持一个或多个受限制的配置文件。

一些受限制的配置文件定义为其他受限制的配置文件的功能的子集 (例如，MPEG2\_配置文件是 MPEG2 的功能的子集\_B 配置文件)。 支持特定的限制配置文件的加速器还必须支持任何受限制的配置文件，而是受支持的配置文件的一部分。 例如，支持 MPEG2 的加速器\_B 配置文件还必须支持 MPEG2\_一个配置文件。

### <a name="span-idnonrestrictedoperationspanspan-idnonrestrictedoperationspanspan-idnonrestrictedoperationspannonrestricted-operation"></a><span id="Nonrestricted_Operation"></span><span id="nonrestricted_operation"></span><span id="NONRESTRICTED_OPERATION"></span>Nonrestricted 的操作

如果在 DirectX VA 加速器使用而无需向受限制的配置文件，严格的一致性**wRestrictedMode**的成员[ **DXVA\_ConnectMode** ](https://msdn.microsoft.com/library/windows/hardware/ff563138)结构必须设置为 0xFFFF 以指示此缺少的限制。

所有定义的值**bDXVA\_Func**允许使用变量。

 

 





