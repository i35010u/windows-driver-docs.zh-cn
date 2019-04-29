---
title: CM_PROB_HELD_FOR_EJECT
description: CM_PROB_HELD_FOR_EJECT
ms.assetid: 8d67ad71-276d-4dea-b3fb-61fedcfba789
keywords:
- CM_PROB_HELD_FOR_EJECT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2b0c9d11d69a885f4ca447ee78f4235702461a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360317"
---
# <a name="cmprobheldforeject"></a>CM_PROB_HELD_FOR_EJECT

此函数保留供系统使用。

设备已准备好弹出。

## <a name="error-code"></a>错误代码

47

### <a name="display-message"></a>显示消息

"Windows 无法使用这个硬件设备因为它已准备好安全删除，但它具有不已从计算机中删除。 （代码 47）"

"若要解决此问题，此设备从计算机中拔出和然后重新插入。

### <a name="recommended-resolution"></a>建议的解决方法

拔出设备并将其插入。 或者，选择**重新启动计算机**将重新启动计算机并使设备可用。

发生此错误应仅当用户调用热即插即用程序，以准备删除设备 (它调用[ **CM_Request_Device_Eject**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_request_device_ejectw))，或如果用户按下物理弹出按钮 （调用[ **IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdeviceeject))。 用户可以准备当前不可删除，如 CD-ROM 困在便携式计算机和停靠的工作站送纸器之间的设备。
