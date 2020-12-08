---
title: 错误报告
description: 错误报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34da710a464a39ae09f3dad4052787e775530278
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818953"
---
# <a name="error-reporting"></a>错误报告





[IWiaMiniDrv 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)中的所有方法都返回 COM HRESULT 值。 如果该方法成功，则微型驱动程序返回 S \_ OK 并清除 *plDevErrVal* 参数指向的设备错误值。 如果该方法失败，微型驱动程序将返回标准 COM 错误代码，并 \* 使用特定于设备的错误代码设置 *plDevErrVal* 。 WIA 服务可以调用 [**IWiaMiniDrv：:D rvgetdeviceerrorstr**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr) 方法，以获取与 *plDevErrVal* 指向的值相关联的错误消息字符串。 有关 COM 错误值的详细信息，请参阅 Microsoft Windows SDK 文档。

 

