---
title: 存储和传输音频数据
description: 存储和传输音频数据
ms.assetid: c8d0af2f-1c3d-49d5-96ca-de1703f85448
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb77c1a22006a25e216c1a863c3ae3ad14eda680
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383718"
---
# <a name="storing-and-transferring-audio-data"></a>存储和传输音频数据





Microsoft Windows Me 和 Windows XP 某些 WIA 驱动程序使用以下三个 WIA 属性用于存储音频数据：

[**WIA\_IPC\_AUDIO\_AVAILABLE**](https://msdn.microsoft.com/library/windows/hardware/ff552530)

[**WIA\_IPC\_AUDIO\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552534)

[**WIA\_IPC\_AUDIO\_DATA\_FORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff552538)

这些属性已过时，并应不再使用。

音频图片项应以附件的形式表示。 这可轻松访问所有 WIA 微型驱动程序支持的音频格式。 与传输 WIA 项树中的其他项相同的方式传输音频内容。

 

 




