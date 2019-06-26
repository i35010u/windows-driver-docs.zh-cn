---
title: 运行默认的 Finish-Install 操作
description: 运行默认的 Finish-Install 操作
ms.assetid: a66d418e-9a66-4c11-854d-6e597ffa01f7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c8e8632430e9d1c261a9636469d9899189be04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378033"
---
# <a name="running-the-default-finish-install-action"></a>运行默认的 Finish-Install 操作


在 Windows 7 中，默认值完成安装操作提供的系统提供[ **SetupDiFinishInstallAction** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))函数。

如果设备不具有类安装程序中，或类安装程序在响应中返回 ERROR_DI_DO_DEFAULT [ **DIF_FINISHINSTALL_ACTION** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-finishinstall-action)请求时，Windows 调用**SetupDiFinishInstallAction**设备的所有安装程序完成其完成安装操作后。

在 Windows 8 和更高版本中，没有默认值完成安装操作。

 

 





