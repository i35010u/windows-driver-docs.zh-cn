---
title: 运行默认的 Finish-Install 操作
description: 运行默认的 Finish-Install 操作
ms.assetid: a66d418e-9a66-4c11-854d-6e597ffa01f7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274653bfc07beb4afe8567b74b71cc2f76587ec7
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094945"
---
# <a name="running-the-default-finish-install-action"></a>运行默认的 Finish-Install 操作


在 Windows 7 中，默认的 "完成-安装" 操作由系统提供的 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85)) 函数提供。

如果设备没有类安装程序，或者类安装程序返回 ERROR_DI_DO_DEFAULT 以响应 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求，则 Windows 将在设备的所有安装程序完成其完成安装操作后调用 **SetupDiFinishInstallAction** 。

在 Windows 8 及更高版本中，没有默认的完成安装操作。

 

