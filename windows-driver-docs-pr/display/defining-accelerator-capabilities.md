---
title: 定义加速器功能
description: 定义加速器功能
ms.assetid: 1f590cfd-74b8-4a08-848d-fcbb2c0c9486
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，加速器功能
- 视频加速 WDK DirectX，加速器功能
- VA WDK DirectX，加速器功能
- 受限配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7d1638a64d80e1e3003bbbd8637c75b3af6f9f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839766"
---
# <a name="defining-accelerator-capabilities"></a>定义加速器功能


## <span id="ddk_defining_accelerator_capabilities_gg"></span><span id="DDK_DEFINING_ACCELERATOR_CAPABILITIES_GG"></span>


加速器可用于受限制的操作，在这种情况下，它符合[受限的配置文件](restricted-profiles.md)，或者可以在 nonrestricted 操作中使用，在这种情况下，它不符合受限制的配置文件。

### <a name="span-idrestricted_operationspanspan-idrestricted_operationspanspan-idrestricted_operationspanrestricted-operation"></a><span id="Restricted_Operation"></span><span id="restricted_operation"></span><span id="RESTRICTED_OPERATION"></span>受限操作

加速器的功能是根据它支持的受限制配置文件定义的。 加速器可以支持一个或多个受限制的配置文件。

一些受限制的配置文件定义为其他受限制配置文件的功能子集（例如，配置文件\_mpeg2\_B 配置文件的功能的子集）。 支持特定限制配置文件的快捷键必须也支持作为受支持配置文件子集的任何受限配置文件。 例如，支持 MPEG2\_B 配置文件的快捷键还必须支持配置文件\_MPEG2。

### <a name="span-idnonrestricted_operationspanspan-idnonrestricted_operationspanspan-idnonrestricted_operationspannonrestricted-operation"></a><span id="Nonrestricted_Operation"></span><span id="nonrestricted_operation"></span><span id="NONRESTRICTED_OPERATION"></span>Nonrestricted 操作

如果在 DirectX VA 中，使用的是不严格符合受限配置文件的加速器，则必须将[**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)结构的**wRestrictedMode**成员设置为0xffff，以指示这种情况缺乏限制。

允许使用**bDXVA\_Func**变量的所有已定义值。

 

 





