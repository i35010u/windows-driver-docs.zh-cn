---
title: 同一硬件上的多个数据流
description: 同一硬件上的多个数据流
ms.assetid: 23133022-6d00-44ad-8c0d-24715204cacc
keywords:
- 多个数据流的 WDK DVD 解码器
- WDK DVD 解码器支持流号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a677d867fc828438dbc0c7c9cb58b396156927e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363281"
---
# <a name="multiple-data-streams-on-the-same-hardware"></a>同一硬件上的多个数据流





许多解码器有几个使用相同的解码器硬件片段的流。 对于这些设备，不需要单独对每个流执行的密钥协商。 若要此信息指示给 DVD 解码器模型，使用[ **KS\_DVDCOPY\_设置\_复制\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)属性。 当此属性上发出 get 操作时，解码器可能会响应以下任一内容：

KS\_DVDCOPYSTATE\_身份验证\_不\_必需

KS\_DVDCOPYSTATE\_身份验证\_必需

KS\_DVDCOPYSTATE\_身份验证\_不\_必需指示给定的流不会不需要的密钥协商，因为在同一硬件上的另一个流已执行它。 例如，如果解码器接收**获取**属性上的音频流首先，使用进行了响应**KS\_DVDCOPYSTATE\_身份验证\_必需**上音频流和**KS\_DVDCOPYSTATE\_身份验证\_不\_REQUIRED**上所有其他流。 后通过身份验证答复\_不\_必需的该流不会收到任何更多密钥交换属性直到下一个标题键进行协商。 此时，解码器可以再次选择回复时使用身份验证\_不\_必需。

若要允许其他应用程序除了在解码器需要在只有一个流上执行版权保护的情况下，播放 DVD 解码器执行协商上要接收的第一个流**获取**属性调用**KS\_DVDCOPY\_设置\_副本\_状态**流打开之后。 请不要对版权保护属性，可以使用只有一个流。

 

 




