---
title: 错误报告
description: 错误报告
ms.assetid: 6f8c08f4-2809-4f49-9332-bbee85399404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f782872739b6cab558436a70a3a66512a82fca78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370056"
---
# <a name="error-reporting"></a>错误报告





中的所有方法[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)返回 COM HRESULT 值。 如果该方法成功，微型驱动程序返回 S\_确定，同时清除设备错误值*plDevErrVal*参数指向。 如果该方法将失败，微型驱动程序将返回标准的 COM 错误代码，并设置\* *plDevErrVal* ，特定于设备的错误代码。 WIA 服务可以调用[ **IWiaMiniDrv::drvGetDeviceErrorStr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr)指向方法来获取与值相关联的错误消息字符串*plDevErrVal*。 有关 COM 错误值的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




