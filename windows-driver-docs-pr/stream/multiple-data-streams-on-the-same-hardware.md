---
title: 同一硬件上的多个数据流
description: 同一硬件上的多个数据流
ms.assetid: 23133022-6d00-44ad-8c0d-24715204cacc
keywords:
- 多数据流 WDK DVD 解码器
- 流数字支持的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86d3b0375e83339d6f8d352c37c2e7427deb506
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842131"
---
# <a name="multiple-data-streams-on-the-same-hardware"></a>同一硬件上的多个数据流





许多解码器具有使用同一解码器硬件的多个流。 对于这些设备，无需对每个流单独执行密钥协商。 若要向 DVD 解码器模型指示这一点，请使用[**KS\_DVDCOPY\_设置\_复制\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)属性。 在此属性上发出 get 操作时，解码器可以使用以下任一方法进行响应：

KS\_DVDCOPYSTATE\_身份验证\_不需要\_

KS\_DVDCOPYSTATE\_身份验证\_必需

KS\_DVDCOPYSTATE\_身份验证\_不\_必需表示给定的流不需要密钥协商，因为同一硬件上的另一个流已经执行了此项协商。 例如，如果解码器首先接收音频流上的**Get**属性，则它将以**KS\_DVDCOPYSTATE\_身份验证\_，** 音频流和 **\_KS 上的 DVDCOPYSTATE\_不\_所有其他流上需要身份验证\_** 。 在对身份验证进行回复之后\_不\_需要，该流在协商下一个标题键之前不会接收更多的密钥交换属性。 此时，解码器可以再次选择通过身份验证进行回复\_不\_需要。

若要允许除 DVD 播放之外的其他应用程序，如果解码器只需对一个流执行版权保护，则解码器将对第一个流执行协商，以接收对 **KS\_DVDCOPY 的 Get 属性调用\_设置流打开后\_复制\_状态**。 不要将版权保护属性硬编码为仅使用一个流。

 

 




