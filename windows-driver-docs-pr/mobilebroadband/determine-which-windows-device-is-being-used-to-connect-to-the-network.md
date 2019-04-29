---
title: 确定设备连接到网络的 Windows
description: 确定正在使用哪个 Windows 设备连接到网络
ms.assetid: ea9a07cd-ad6e-4c49-aae0-fc9eee9b17c8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6973e43207f189d87be8d71a3a6917da268c73eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378321"
---
# <a name="determine-which-windows-device-is-being-used-to-connect-to-the-network"></a>确定正在使用哪个 Windows 设备连接到网络

若要确定哪个 Windows 设备用于连接到网络，请检查网络适配器，这公开的 Windows 设备 ID [ **DeviceId** ](https://msdn.microsoft.com/library/windows/apps/br207365)当前的网络设备的属性帐户的对象。

例如：

``` syntax
account.currentDeviceInformation.deviceId
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






