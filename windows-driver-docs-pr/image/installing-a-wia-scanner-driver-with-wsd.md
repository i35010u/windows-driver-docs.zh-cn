---
title: 使用 WSD 安装 WIA 扫描仪驱动程序
description: 使用 WSD 安装 WIA 扫描仪驱动程序
ms.assetid: 7dc125cb-0f20-4d3d-8124-df556a9644d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dbb6935133e0e2d860e2273751c5324e30e3e30
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191687"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>使用 WSD 安装 WIA 扫描仪驱动程序


若要使用 WSD 安装 WIA 扫描器驱动程序，你应该使用 Windows Vista 中提供的 *WSDScan.sys* 内核模式驱动程序。 在 IRP \_ MN \_ 启动 \_ 设备期间， *WSDScan.sys* 读取 PKEY \_ PNPX \_ ID 设备属性，并将其保存到注册表中。 设备属性将写入设备密钥，该设备密钥在要安装的映像设备的注册表中创建，并将其写入 **CreateFileName** wia 注册表值 (这将在 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md)) 中介绍。 当在[**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)方法期间进行[**IStiDeviceControl：： GetMyDevicePortName**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)调用时，wia 服务会将此值返回到 wia 微型驱动程序。

使用 *WSDScan.sys* 的 web service 扫描器的 WIA 微型驱动程序在安装设备时已初始化其 **CreateFileName** 值。 若要初始化此值，WIA 微型驱动程序的 INF 文件必须引用**STI。WSDSection**和**STI。WSDSection**在微型驱动程序 inf 文件的 "**安装**" 和 "**服务**" 部分中的*Sti*文件中，如[Web 服务扫描器的示例 inf 文件](sample-inf-file-for-a-web-services-scanner.md)中所示。

 

