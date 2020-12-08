---
title: 音频微型端口辅助接口
description: 音频微型端口辅助接口
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b7d111de30c1f238da33ce2a4698182c99cc9dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789395"
---
# <a name="audio-miniport-auxiliary-interfaces"></a>音频微型端口辅助接口


## <span id="ddk_audio_miniport_auxiliary_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_AUXILIARY_INTERFACES_KS"></span>


某些微型端口驱动程序支持可选的辅助接口，并提供对专用微型端口驱动程序功能的访问权限。 本部分介绍由微型端口驱动程序实现并向端口驱动程序公开的辅助接口。

本节将讨论以下接口：

[IMusicTechnology](/windows-hardware/drivers/ddi/portcls/nn-portcls-imusictechnology)-用于更改 dmu 微型端口驱动程序的 pin 的数据范围中指定的 DirectMusic 合成器技术。

[IPinCount](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipincount) -为微型端口驱动程序提供了一种动态监视和操作其 pin 计数的方法。

[IPinName](/windows-hardware/drivers/ddi/portcls/nf-portcls-ipinname-getpinname) -允许端口驱动程序动态更新终结点的名称。

[IAdapterPnpManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement) -允许适配器注册以接收 PnP 管理消息。

 

