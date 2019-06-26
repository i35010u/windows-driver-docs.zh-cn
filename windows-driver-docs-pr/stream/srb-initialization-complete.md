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
ms.openlocfilehash: 257899c40a33b83ebdf0da4b2c8114f167733e5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377911"
---
# <a name="srbinitializationcomplete"></a>SRB\_初始化\_完成


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


在类驱动程序将发送此请求，以指示它已完成其初始化微型驱动程序。

### <a name="comments"></a>备注

在类驱动程序微型驱动程序完成此请求，可以开始发送[ **SRB\_打开\_流**](srb-open-stream.md)请求。

当微型驱动程序收到此 SRB 时，微型驱动程序应创建任何必要的注册表项。 例如，DirectShow 筛选器可能会注册一个电视调谐器或纵横制用于筛选图形时发生使用[ **StreamClassRegisterFilterWithNoKSPins** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisterfilterwithnokspins)例程。

 

 





