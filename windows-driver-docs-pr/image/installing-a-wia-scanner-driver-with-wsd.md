---
title: 使用 WSD 安装 WIA 扫描仪驱动程序
description: 使用 WSD 安装 WIA 扫描仪驱动程序
ms.assetid: 7dc125cb-0f20-4d3d-8124-df556a9644d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc0277e287db194a6fe60ec5dc70024b49c03568
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378933"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>使用 WSD 安装 WIA 扫描仪驱动程序


若要使用 WSD 安装 WIA 扫描程序驱动程序，应使用*WSDScan.sys*内核模式驱动程序，作为 Windows Vista 的一部分提供。 期间 IRP\_MN\_启动\_设备*WSDScan.sys*读取主键\_PNPX\_ID 设备属性并将其保存到注册表。 设备属性写入到映像正在安装的设备以及在注册表中创建的设备密钥**CreateFileName** WIA 注册表值 (中所述[WIA 设备 INF 文件](inf-files-for-wia-devices.md)). 此值将由 WIA 服务返回到 WIA 微型驱动程序时[ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)调用期间[ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)方法。

WIA 微型驱动程序使用 web 服务扫描程序*WSDScan.sys*具有其**CreateFileName**初始化安装设备时的值。 若要初始化此值，WIA 微型驱动程序的 INF 文件必须引用**STI。WSDSection**和**STI。WSDSection.Services**从*Sti.inf*中的文件**安装**并**服务**微型驱动程序 INF 文件，如中所示的各个部分[对 Web 服务扫描程序示例 INF 文件](sample-inf-file-for-a-web-services-scanner.md)。

 

 




