---
title: 运行默认完成安装操作
description: 运行默认完成安装操作
ms.assetid: a66d418e-9a66-4c11-854d-6e597ffa01f7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30028e3f394b7bb508846638e905a9ef3a91bb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524563"
---
# <a name="running-the-default-finish-install-action"></a>运行默认完成安装操作


在 Windows 7 中，默认值完成安装操作提供的系统提供[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)函数。

如果设备不具有类安装程序中，或类安装程序在响应中返回 ERROR_DI_DO_DEFAULT [ **DIF_FINISHINSTALL_ACTION** ](https://msdn.microsoft.com/library/windows/hardware/ff543684)请求时，Windows 调用**SetupDiFinishInstallAction**设备的所有安装程序完成其完成安装操作后。

在 Windows 8 和更高版本中，没有默认值完成安装操作。

 

 





