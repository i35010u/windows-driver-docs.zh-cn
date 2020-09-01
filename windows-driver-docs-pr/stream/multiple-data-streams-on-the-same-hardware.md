---
title: 同一硬件上的多个数据流
description: 同一硬件上的多个数据流
ms.assetid: 23133022-6d00-44ad-8c0d-24715204cacc
keywords:
- 多数据流 WDK DVD 解码器
- 流数字支持的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd05a35149e1930e2d490e20ac39821d51c2a826
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188735"
---
# <a name="multiple-data-streams-on-the-same-hardware"></a>同一硬件上的多个数据流





许多解码器具有使用同一解码器硬件的多个流。 对于这些设备，无需对每个流单独执行密钥协商。 若要向 DVD 解码器模型指示这一点，请使用 [**KS \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state) 属性。 在此属性上发出 get 操作时，解码器可以使用以下任一方法进行响应：

\_ \_ \_ 不需要 KS DVDCOPYSTATE 身份验证 \_

\_需要 DVDCOPYSTATE \_ AUTHENTICATION 身份验证 \_

KS \_ DVDCOPYSTATE \_ AUTHENTICATION \_ 不 \_ 需要，表示给定的流不需要密钥协商，因为同一硬件上的另一个流已经执行了此功能。 例如，如果解码器首先接收音频流上的 **Get** 属性，则会在音频流上 ** \_ 要求 ks \_ DVDCOPYSTATE \_ authentication** ，而在所有其他流上 ** \_ \_ \_ 不 \_ 需要 ks DVDCOPYSTATE authentication** 。 在不要求进行身份验证的情况 \_ \_ 下，在协商下一个标题键之前，该流不会接收更多的密钥交换属性。 此时，解码器可能会再次选择 "不需要身份验证" 进行回复 \_ \_ 。

若要允许除 DVD 播放之外的其他应用程序，如果解码器只需对一个流执行版权保护，则解码器会对第一个流执行协商，以便在流打开后接收**KS \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态**的**Get**属性调用。 不要将版权保护属性硬编码为仅使用一个流。

 

