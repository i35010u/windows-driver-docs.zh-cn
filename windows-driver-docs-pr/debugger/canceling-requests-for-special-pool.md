---
title: 取消针对特殊池的请求
description: 取消针对特殊池的请求
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a89df8094a24ef9c462cafc30a95c769328268f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788847"
---
# <a name="canceling-requests-for-special-pool"></a>取消针对特殊池的请求


## <span id="ddk_canceling_requests_for_special_pool_dtools"></span><span id="DDK_CANCELING_REQUESTS_FOR_SPECIAL_POOL_DTOOLS"></span>


如果请求是通过使用 GFlags 进行的，则可以使用 GFlags 取消从特殊池进行分配的请求。 不能使用 GFlags 来取消对使用驱动程序验证程序进行的特殊池的请求。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来取消特殊的池请求。 有关信息，请参阅 [**GFlags 命令**](gflags-commands.md)。

**取消对特殊池的请求**

1.  选择 "系统注册表" 选项卡或 "内核标志" 选项卡。

    在 Windows Vista 和更高版本的 Windows 上，此选项在两个选项卡上都可用。 在早期版本的 Windows 上，它仅在 " **系统注册表** " 选项卡上可用。

2.  从 " **内核特殊池标记** " 框中删除文本或十六进制值。

3.  单击“应用” 。

 

 





