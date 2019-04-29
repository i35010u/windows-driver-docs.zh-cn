---
title: PTP 错误代码
description: PTP 错误代码
ms.assetid: 4d7ad081-fc0b-4a9e-8f17-a0c98fa4fa50
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca63726c0b5604ec167b8d3fc34a2c5c2d6d786
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379627"
---
# <a name="ptp-error-codes"></a>PTP 错误代码





当 Microsoft PTP WIA 微型驱动程序检测到错误时，它将响应代码传递给 WIA。 如果 PTP 照相机返回 0x2001 （正常） 以外的响应，WIA 微型驱动程序返回包装成一个 HRESULT 错误代码的响应代码。 错误代码的格式为 0x8004XXXX，其中 XXXX 表示响应代码的四个十六进制数字。 这是设计用于特定 PTP 照相机的 WIA 应用程序非常有用。 错误/状态信息时保留的丰富的状态报告给最终用户。

 

 




