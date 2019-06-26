---
title: 音频微型端口辅助接口
description: 音频微型端口辅助接口
ms.assetid: cda22e86-f3f7-430c-856d-a2c868caa975
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15180ea52e96ee0759501206825a5727817296ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355686"
---
# <a name="audio-miniport-auxiliary-interfaces"></a>音频微型端口辅助接口


## <span id="ddk_audio_miniport_auxiliary_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_AUXILIARY_INTERFACES_KS"></span>


某些微型端口驱动程序支持都是可选的辅助接口，并提供专用的微型端口驱动程序功能的访问权限。 本部分介绍由微型端口驱动程序实现并向端口驱动程序公开的辅助接口。

在本部分中讨论了以下接口：

[IMusicTechnology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-imusictechnology)-用于更改 Dmu 微型端口驱动程序的 pin 的数据范围中指定的 DirectMusic 合成器技术。

[IPinCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipincount) -提供一种微型端口驱动程序，以动态地监视和管理其 pin 计数。

[IPinName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-ipinname-getpinname) -允许端口驱动程序，以动态更新的终结点的名称。

[IAdapterPnpManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpnpmanagement) -允许管理消息的适配器注册以接收即插即用。

 

 





