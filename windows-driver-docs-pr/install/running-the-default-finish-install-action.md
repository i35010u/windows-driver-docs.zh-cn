---
title: 运行默认的 Finish-Install 操作
description: 运行默认的 Finish-Install 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b23de084b39940b97679b174ee178ef3a19051d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824427"
---
# <a name="running-the-default-finish-install-action"></a>运行默认的 Finish-Install 操作


在 Windows 7 中，默认的 "完成-安装" 操作由系统提供的 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85)) 函数提供。

如果设备没有类安装程序，或者类安装程序返回 ERROR_DI_DO_DEFAULT 以响应 [**DIF_FINISHINSTALL_ACTION**](./dif-finishinstall-action.md) 请求，则 Windows 将在设备的所有安装程序完成其完成安装操作后调用 **SetupDiFinishInstallAction** 。

在 Windows 8 及更高版本中，没有默认的完成安装操作。

 

