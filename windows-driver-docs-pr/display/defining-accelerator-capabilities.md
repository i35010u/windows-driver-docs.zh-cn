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
ms.openlocfilehash: bc34214ccb0f1afcfac974dc757521084da3dc30
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065496"
---
# <a name="defining-accelerator-capabilities"></a>定义加速器功能


## <span id="ddk_defining_accelerator_capabilities_gg"></span><span id="DDK_DEFINING_ACCELERATOR_CAPABILITIES_GG"></span>


加速器可用于受限制的操作，在这种情况下，它符合 [受限的配置文件](restricted-profiles.md)，或者可以在 nonrestricted 操作中使用，在这种情况下，它不符合受限制的配置文件。

### <a name="span-idrestricted_operationspanspan-idrestricted_operationspanspan-idrestricted_operationspanrestricted-operation"></a><span id="Restricted_Operation"></span><span id="restricted_operation"></span><span id="RESTRICTED_OPERATION"></span>受限操作

加速器的功能是根据它支持的受限制配置文件定义的。 加速器可以支持一个或多个受限制的配置文件。

一些受限制的配置文件被定义为其他受限制配置文件的功能的子集 (例如，MPEG2 \_ A profile 是 mpeg2 \_ B profile) 功能的子集。 支持特定限制配置文件的快捷键必须也支持作为受支持配置文件子集的任何受限配置文件。 例如，支持 MPEG2 \_ B 配置文件的快捷键还必须支持 mpeg2 \_ A profile。

### <a name="span-idnonrestricted_operationspanspan-idnonrestricted_operationspanspan-idnonrestricted_operationspannonrestricted-operation"></a><span id="Nonrestricted_Operation"></span><span id="nonrestricted_operation"></span><span id="NONRESTRICTED_OPERATION"></span>Nonrestricted 操作

如果在 DirectX VA 中，将使用不严格符合受限配置文件的加速器，则必须将[**DXVA \_ ConnectMode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)结构的**WRestrictedMode**成员设置为0xffff，以指示这种情况缺乏限制。

允许使用 **bDXVA \_ Func** 变量的所有已定义值。

 

