---
title: OPM 和显示模式
description: OPM 和显示模式
ms.assetid: d412a32b-7afd-4f48-9b8e-7cf66533349f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8afd9ce98d10af898f3bba37ebf7675f62b64e48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547179"
---
# <a name="opm-and-display-modes"></a>OPM 和显示模式


显示微型端口驱动程序应报告所有与受保护的输出，而不考虑当前正在使用的显示模式相关联的物理连接器支持的保护类型。 当接收到的调用时，显示微型端口驱动程序报告支持的保护类型及其[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)或[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)函数与 DXGKMDT\_OPM\_获取\_支持\_保护\_中设置的类型**guidInformation**的成员[ **DXGKMDT\_OPM\_获取\_信息\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560868)结构。 有关检索支持的详细信息的保护类型，请参阅[检索有关受保护的输出的信息](retrieving-information-about-a-protected-output.md)或[有关保护输出检索 COPP 兼容信息](retrieving-copp-compatible-information-about-a-protected-output.md)。

如果当前的分辨率太高，特定的保护类型，该驱动程序应返回的错误时显示微型端口驱动程序[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)调用函数若要为该保护类型设置保护级别。 以下方案提供情形的示例驱动程序的*DxgkDdiOPMConfigureProtectedOutput*函数应返回成功消息和错误时：

-   如果受保护的输出将是 S-视频输出接口，显示微型端口驱动程序的调用与相关联*DxgkDdiOPMGetCOPPCompatibleInformation*函数与 DXGKMDT\_OPM\_GET\_支持\_保护\_类型集应指示模拟内容保护 (ACP) 类型的支持 (DXGKMDT\_OPM\_保护\_类型\_ACP)。 此后，如果驱动程序的*DxgkDdiOPMConfigureProtectedOutput*函数调用设置一个级别的 ACP 类型的此连接器，则驱动程序应返回成功，因为固定的 S-视频输出分辨率，即使桌面分辨率 （显示模式） 可能会更高版本。

-   如果受保护的输出与组件输出连接器，显示微型端口驱动程序的调用相关联*DxgkDdiOPMGetCOPPCompatibleInformation*函数与 DXGKMDT\_OPM\_GET\_支持\_保护\_类型集还应该指示 ACP 类型的支持。 但是，如果驱动程序的*DxgkDdiOPMConfigureProtectedOutput*调用函数时显示分辨率为 720p 或 1080i ACP 类型在此输出上设置级别，则驱动程序应返回状态\_图形\_OPM\_解析\_过\_高错误代码。 720p 或 1080i 得太高的分辨率设置保护级别的 ACP 类型设置为的组件输出连接器。

 

 





