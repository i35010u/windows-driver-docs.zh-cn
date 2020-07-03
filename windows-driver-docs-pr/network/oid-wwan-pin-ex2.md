---
title: OID_WWAN_PIN_EX2
description: OID_WWAN_PIN_EX2 访问 UICC 线性固定或循环文件，其结构类型为 WwanUiccFileStructureCyclic 或 WwanUiccFileStructureLinear。
ms.assetid: F5D0A1B8-4D7E-469A-B738-2965D254868E
ms.date: 04/10/2019
keywords:
- 从 Windows Vista 开始 OID_WWAN_PIN_EX2 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 95230980572820cea51d20b39ca7872ba41de51d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918131"
---
# <a name="oid_wwan_pin_ex2"></a>OID_WWAN_PIN_EX2

OID_WWAN_PIN_EX2 设置或返回与个人标识号（Pin）相关的扩展信息。 OID_WWAN_PIN_EX2 类似于[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)，但扩展它以支持多应用 UICC 卡。

查询负载包含一个[**NDIS_WWAN_PIN_APP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)结构，该结构指定正在查询其 PIN 的目标应用程序 ID。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状态通知，其中包含描述应用程序的 PIN 的[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)结构。 

设置负载包含指定要为应用程序执行的 PIN 操作的[**NDIS_WWAN_SET_PIN_EX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)结构。 微型端口驱动程序必须异步处理设置请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状态通知，其中包含描述应用程序的 PIN 状态的[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)结构。

## <a name="remarks"></a>备注

仅支持单一验证功能的 UICCs。 不支持支持多个应用程序 PIN 的多验证功能的 UICCs。 将一个应用程序 PIN （PIN1）分配给 UICC 上的所有 ADFs/DFs 和文件。 但是，每个应用程序都可以将本地 PIN （PIN2）指定为级别2用户验证要求，因此需要对每个访问命令进行其他验证。 OID_WWAN_PIN_EX2 支持此方案。

与[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)一样，OID_WWAN_PIN_EX2 设备一次只报告一个 PIN。 如果启用多个 Pin 并报告多个 Pin，则微型端口驱动程序必须先报告 PIN1。 例如，如果启用了 subsidy 锁定报告并启用了 SIM 的 PIN1，则仅在通过将**PinSize**设置为零（0）指定 PIN1 后，才应在后续查询请求中报告 SUBSIDY 锁定 PIN。 在这种情况下，集请求类似于查询，并返回引用的 PIN 状态。 这与 "验证" 命令的行为完全一致，如 " [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)" 的 "11.1.9" 部分中所指定。

有关此 OID 的用法的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)

[**NDIS_WWAN_PIN_APP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)

[**NDIS_WWAN_SET_PIN_EX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)

[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)
