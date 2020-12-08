---
title: PTP 错误代码
description: PTP 错误代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39e68d9a69d18cdde4839687d77b36ca9d53ef00
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829603"
---
# <a name="ptp-error-codes"></a>PTP 错误代码





当 Microsoft PTP WIA 微型驱动程序检测到错误时，它会将响应代码传递到 WIA。 如果 PTP 相机返回除 0x2001 (OK) 以外的响应，则 WIA 微型驱动程序会返回包装为 HRESULT 错误代码的响应代码。 错误代码的格式为0x8004XXXX，其中 XXXX 表示响应代码的四个十六进制数字。 这对于旨在使用特定 PTP 相机的 WIA 应用程序非常有用。 将保留错误/状态信息以便向最终用户报告丰富的状态。

 

 




