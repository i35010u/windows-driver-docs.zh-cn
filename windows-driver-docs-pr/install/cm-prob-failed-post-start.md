---
title: CM_PROB_FAILED_POST_START
description: CM_PROB_FAILED_POST_START
ms.assetid: 82d43c8b-d5de-4395-9ca0-34d2258b9772
keywords:
- CM_PROB_FAILED_POST_START
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54b4df29184de0203e117d31d1777dd9a0b51882
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391484"
---
# <a name="cmprobfailedpoststart"></a>CM_PROB_FAILED_POST_START

此函数保留供系统使用。

驱动程序报告设备失败。

## <a name="error-code"></a>错误代码

43

### <a name="display-message"></a>显示消息

"Windows 已停止，此设备因为它已报告问题。 （代码 43）"

### <a name="recommended-resolution"></a>建议的解决方法

卸载并重新安装该设备。

控制设备的驱动因素之一告诉该设备以某种方式 IRP_MN_QUERY_PNP_DEVICE_STATE 响应失败的操作系统。
