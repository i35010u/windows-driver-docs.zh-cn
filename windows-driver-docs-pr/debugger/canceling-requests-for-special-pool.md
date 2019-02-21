---
title: 为特殊池取消请求
description: 为特殊池取消请求
ms.assetid: fb18cb15-33ee-4e6d-856e-70c4ffbf8383
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d19940f4cc708eb9421d8641aa75554ba92c273
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523039"
---
# <a name="canceling-requests-for-special-pool"></a>为特殊池取消请求


## <span id="ddk_canceling_requests_for_special_pool_dtools"></span><span id="DDK_CANCELING_REQUESTS_FOR_SPECIAL_POOL_DTOOLS"></span>


GFlags 可用于取消对特殊池中分配的请求，如果通过使用 GFlags 发出请求。 不能使用 GFlags 来取消可能由使用驱动程序验证程序的特殊池的请求。

在 Windows Vista 和更高版本的 Windows 中，您还可以使用命令行取消特殊池请求。 有关信息，请参阅[ **GFlags 命令**](gflags-commands.md)。

**若要取消的特殊池请求**

1.  选择系统注册表选项卡或内核标志选项卡。

    在 Windows Vista 和更高版本的 Windows 上，此选项才可用两个选项卡。 在早期版本的 Windows，它是仅适用于**系统注册表**选项卡。

2.  删除文本或十六进制值从**内核特殊池标记**框。

3.  单击 **“应用”**。

 

 





