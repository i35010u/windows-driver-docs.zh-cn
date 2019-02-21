---
title: SRB\_初始化\_完成
description: SRB\_初始化\_完成
ms.assetid: 72412ab0-226d-4bf6-af6b-98d62653e061
keywords:
- SRB_INITIALIZATION_COMPLETE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_INITIALIZATION_COMPLETE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4eaeb70035b5057b21ca60f0cf244c527bc8f91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521690"
---
# <a name="srbinitializationcomplete"></a>SRB\_初始化\_完成


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


在类驱动程序将发送此请求，以指示它已完成其初始化微型驱动程序。

### <a name="comments"></a>备注

在类驱动程序微型驱动程序完成此请求，可以开始发送[ **SRB\_打开\_流**](srb-open-stream.md)请求。

当微型驱动程序收到此 SRB 时，微型驱动程序应创建任何必要的注册表项。 例如，DirectShow 筛选器可能会注册一个电视调谐器或纵横制用于筛选图形时发生使用[ **StreamClassRegisterFilterWithNoKSPins** ](https://msdn.microsoft.com/library/windows/hardware/ff568261)例程。

 

 





