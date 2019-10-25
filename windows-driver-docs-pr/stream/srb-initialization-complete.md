---
title: SRB\_初始化\_完成
description: SRB\_初始化\_完成
ms.assetid: 72412ab0-226d-4bf6-af6b-98d62653e061
keywords:
- SRB_INITIALIZATION_COMPLETE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_INITIALIZATION_COMPLETE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32907a78c00b46bbdf62ff5a8d5ef265e74c1847
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843298"
---
# <a name="srb_initialization_complete"></a>SRB\_初始化\_完成


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


类驱动程序发送此请求，通知微型驱动程序已完成初始化。

### <a name="comments"></a>备注

微型驱动程序完成此请求后，类驱动程序可以开始发送[**SRB\_打开\_流**](srb-open-stream.md)请求。

如果微型驱动程序接收到此 SRB，微型驱动程序应创建任何必需的注册表项。 例如，DirectShow 过滤器可以使用[**StreamClassRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins)例程注册电视调谐器或十字，以便与 FilterGraph 一起使用。

 

 





