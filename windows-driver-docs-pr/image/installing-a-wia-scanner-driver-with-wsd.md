---
title: 使用 WSD 安装 WIA 扫描仪驱动程序
description: 使用 WSD 安装 WIA 扫描仪驱动程序
ms.assetid: 7dc125cb-0f20-4d3d-8124-df556a9644d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d48352a0bbdc9b4a5eea87a7b84035d9bc901565
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840817"
---
# <a name="installing-a-wia-scanner-driver-with-wsd"></a>使用 WSD 安装 WIA 扫描仪驱动程序


若要使用 WSD 安装 WIA 扫描器驱动程序，应使用 Windows Vista 中提供的*WSDScan*内核模式驱动程序。 在 IRP\_MN\_启动\_设备， *WSDScan*读取 PKEY\_PNPX\_ID 设备属性，并将其保存到注册表。 设备属性将写入设备密钥，该设备密钥在要安装的映像设备的注册表中创建，并将其写入到**CreateFileName** wia 注册表值（ [Wia 设备的 INF 文件](inf-files-for-wia-devices.md)中介绍）。 当在[**IStiUSD：： Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)方法期间进行[**IStiDeviceControl：： GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)调用时，wia 服务会将此值返回到 wia 微型驱动程序。

使用*WSDScan*的 web 服务扫描程序的 WIA 微型驱动程序在安装设备时已初始化其**CreateFileName**值。 若要初始化此值，WIA 微型驱动程序的 INF 文件必须引用**STI。WSDSection**和**STI。WSDSection**在微型驱动程序 inf 文件的 "**安装**" 和 "**服务**" 部分中的*Sti*文件中，如[Web 服务扫描器的示例 inf 文件](sample-inf-file-for-a-web-services-scanner.md)中所示。

 

 




