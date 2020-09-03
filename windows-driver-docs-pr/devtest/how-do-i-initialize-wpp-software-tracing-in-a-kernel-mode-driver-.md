---
title: 如何实现在内核模式驱动程序中初始化 WPP 软件跟踪
description: 如何实现在内核模式驱动程序中初始化 WPP 软件跟踪
ms.assetid: 739428e8-14ff-4435-80e6-35b5c3366c79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55bd39da18d766252e4b5fc02bc5f5742e51826e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384539"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-kernel-mode-driver"></a>如何在内核模式驱动程序中初始化 WPP 软件跟踪？


您可以通过调用 [wpp \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏初始化 wpp 软件跟踪，在内核模式驱动程序中初始化 wpp 跟踪。

若要避免错误，应在驱动程序的[**DriverEntry**](../storage/driverentry-of-ide-controller-minidriver.md)函数中调用[WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏。

 

