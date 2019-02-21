---
title: 错误报告
description: 错误报告
ms.assetid: 6f8c08f4-2809-4f49-9332-bbee85399404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b46db726be28d391464b342cbe3fbc6a9f6fd15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523958"
---
# <a name="error-reporting"></a>错误报告





中的所有方法[IWiaMiniDrv 接口](https://msdn.microsoft.com/library/windows/hardware/ff545027)返回 COM HRESULT 值。 如果该方法成功，微型驱动程序返回 S\_确定，同时清除设备错误值*plDevErrVal*参数指向。 如果该方法将失败，微型驱动程序将返回标准的 COM 错误代码，并设置\* *plDevErrVal* ，特定于设备的错误代码。 WIA 服务可以调用[ **IWiaMiniDrv::drvGetDeviceErrorStr** ](https://msdn.microsoft.com/library/windows/hardware/ff543982)指向方法来获取与值相关联的错误消息字符串*plDevErrVal*。 有关 COM 错误值的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




